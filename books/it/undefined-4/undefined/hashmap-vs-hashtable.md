# HashMap vs HashTable

\[ 문제 ]

* Hash란?
* HashMap이란?
* HashTable이란?
* HashMap vs HashTable
* ConcurrentHashMap

\[ 정답 ]

*   해설

    #### Hash란?

    * 일종의 변환 함수로, 임의의 크기를 가진 데이터를 받아서 고정된 크기의 값으로 변환 시킴
    * 이 변환된 값을 일반적으로 해시 코드(HashCode), 또는 해시 값(Hash value)라고 부름
    * 동일한 값에 대해선 항상 동일한 해시 값이 생성됨
      * 따라서 같은 데이터에 대해서는 항상 같은 위치에 저장됨

    #### HashMap이란?

    * Map 인터페이스로 구현한 컬렉션
    * Map 인터페이스는 Key 값과 Value 값을 묶어서 하나의 entry(한 쌍)로 저장
    * Key값을 기반으로 데이터를 저장하고 접근하기 때문에, Key값은 항상 Unique 해야함
    * 저장된 순서와 출력 **순서를 보장하지 않는** 데이터 구조
      * Key값에 따른 순서를 보장하고 싶다면 LinkedHashMap 사용

    #### HashTable이란?

    * HashMap과 내부 구조가 동일함 (Map을 인터페이스로 구현한 컬렉션)

    #### HashMap vs HashTable

    <figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

    * Java11 기준이며, HashMap은 key, value 모두 null값을 허용합니다.

    #### Concurrent HashMap

    * 멀티 스레드한 환경을 제공하는 Concurrent 클래스
    *   코드 보기

        ```java
        public class ConcurrentHashMap<K,V> extends AbstractMap<K,V>
            implements ConcurrentMap<K,V>, Serializable {

            public V get(Object key) {}

            public boolean containsKey(Object key) { }

            public V put(K key, V value) {
                return putVal(key, value, false);
            }

            final V putVal(K key, V value, boolean onlyIfAbsent) {
                if (key == null || value == null) throw new NullPointerException();
                int hash = spread(key.hashCode());
                int binCount = 0;
                for (Node<K,V>[] tab = table;;) {
                    Node<K,V> f; int n, i, fh;
                    if (tab == null || (n = tab.length) == 0)
                        tab = initTable();
                    else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
                        if (casTabAt(tab, i, null,
                                     new Node<K,V>(hash, key, value, null)))
                            break;                   // no lock when adding to empty bin
                    }
                    else if ((fh = f.hash) == MOVED)
                        tab = helpTransfer(tab, f);
                    else {
                        V oldVal = null;
                        synchronized (f) {
                            if (tabAt(tab, i) == f) {
                                if (fh >= 0) {
                                    binCount = 1;
                                    for (Node<K,V> e = f;; ++binCount) {
                                        K ek;
                                        if (e.hash == hash &&
                                            ((ek = e.key) == key ||
                                             (ek != null && key.equals(ek)))) {
                                            oldVal = e.val;
                                            if (!onlyIfAbsent)
                                                e.val = value;
                                            break;
                                        }
                                        Node<K,V> pred = e;
                                        if ((e = e.next) == null) {
                                            pred.next = new Node<K,V>(hash, key,
                                                                      value, null);
                                            break;
                                        }
                                    }
                                }
                                else if (f instanceof TreeBin) {
                                    Node<K,V> p;
                                    binCount = 2;
                                    if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key,
                                                                   value)) != null) {
                                        oldVal = p.val;
                                        if (!onlyIfAbsent)
                                            p.val = value;
                                    }
                                }
                            }
                        }
                        if (binCount != 0) {
                            if (binCount >= TREEIFY_THRESHOLD)
                                treeifyBin(tab, i);
                            if (oldVal != null)
                                return oldVal;
                            break;
                        }
                    }
                }
                addCount(1L, binCount);
                return null;
            }
        }
        ```
    * 코드를 보면 알 수있듯이, HashTable과는 다르게 synchronized 키워드가 메서드 전체에 붙어있지 않음
      * get()에는 없고, put()에는 중간에 있음
    * 따라서 읽기 작업은 _**여러 쓰레드가 동시에 할 수 있지만, 쓰기 작업에는 특정 세그먼트 or 버킷에 대한 Lock을 사용**_

Ref

* ConcurrentHashMap 참고 자료 : [https://devlog-wjdrbs96.tistory.com/269](https://devlog-wjdrbs96.tistory.com/269)
