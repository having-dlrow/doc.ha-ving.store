# B-Tree , B+Tree

### 개념

1. 균형이진트리 **탐색 트리**의 일종이다.
2. **정렬목적**으로 사용한다.

#### 이진트리 종류

| 정이진트리  | 모든 노드가 0 혹은 2 자식을 가진 경우 |
| ------ | ----------------------- |
| 완전이진트리 | 마지막 노드까지 순서대로 채워진 트리    |
| 포화이진트리 | 모든 leaf 노드가 꽉찬 트        |
| 균형이진트리 | 최대 1레벨까지만 만드는 트리        |

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### B-Tree, B+Tree 사용

* 데이터 베이스에서 검색 속도를 위해 B+Tree 구조를 채택한다.
* 파일 시스템에서 주로 사용

| B-Tree | CouchDB, MongoDB          |
| ------ | ------------------------- |
| B+Tree | Oracle, Mysql, Postgresql |

#### B-Tree

1. 노드가 적어도 2개 이상의 자식을 갖는다.
2. 정렬이 되도록 저장한다.
3. 최악 복잡도 O(logN)이다.
4. 정해친 차수를 유지 하기 위해, 노드를 이동시킨다.
5. 대량의 데이터를 처리해야 하는 검색 구조인 경우 하나의 노드에 많은 데이터를 가질 수 있다는 점은 큰 장점

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

차수 : 3

ex) **13**이 들어오면

1. 12 하위에 13이 들어가야 한다. (불가)
2. 14 자리에 13이 들어간다.
3. 13노드는 14 자식을 가진다.

#### B+Tree

1. leaf 노드를 LinkedList로 작성
2. leaf 노드만 값을 저장한다. ( B-Tree는 모든 노드가 저장 )
3. leaf 노드만 선형적으로 검사 ( 보다 검색이 빠른 이유 )
4. B-Tree 보다 삽입/삭제에 이점을 가진다.

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

Ref

* [https://www.youtube.com/watch?v=bqkcoSm\_rCs](https://www.youtube.com/watch?v=bqkcoSm\_rCs)
* [https://velog.io/@emplam27/자료구조-그림으로-알아보는-B-Tree](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree)
* [https://escapefromcoding.tistory.com/731](https://escapefromcoding.tistory.com/731)
