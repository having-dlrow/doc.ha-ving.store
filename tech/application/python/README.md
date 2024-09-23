# 🎁 Python

{% embed url="https://wikidocs.net/11" %}

| 데이터 구조                                           |          | 순서 유지 | 중복 허용  | 가변 |
| ------------------------------------------------ | -------- | ----- | ------ | -- |
| Tuple                                            | (a,b,c)  | O     | O      | X  |
| <mark style="background-color:blue;">List</mark> | \[a,b,c] | O     | O      | O  |
| Dictionary                                       | {K:V}    | O     | 키 중복 X | O  |
| Set                                              | {a,b,c}  | X     | X      | O  |

## List

* <mark style="background-color:blue;">`[a,b]형태`</mark>

```

>>> s1  = set([30,2,13])
>>> s1
{2, 13, 30}

>>> li = list(s1)
>>> li
[2, 13, 30]

>>> type(li)
<class 'list'>

>>> tu = tuple(s1)
>>> tu
(2, 13, 30)

>>> type(tu)
<class 'tuple'>
```

## Tuple

* `(1,2)` 형태

```
>>> a = (1)
>>> type(a)
<class 'int'>

>>> a = ('1')
>>> type(a)
<class 'str'>

>>> a = (1,)
>>> type(a)
<class 'tuple'>

>>> a  = '11','22','33','44'
>>> type(a)
<class 'tuple'>
```

## Dictionary

* `{a,b}` 형태
* get(), set()

```
>>> c
{'test': '춘향이'}

>>> c.get('test')
'춘향이'

>>> c.get('test1')


>>> c['test2'] = ['t','e', 's','t']

>>> c
{'test': '춘향이', 'test2': ['t', 'e', 's', 't']}

>>> c.get('test2')[2]
's'

>>> type(c.get('test'))
<class 'str'>

>>> type(c.get('test2')[2])
<class 'str'>

>>> type(c.get('test3')[2])
Traceback (most recent call last):
 File "<stdin>", line 1, in <module>
TypeError: 'NoneType' object is not subscriptable


>>> c.get('test3'[2],'null')    // get() 함수는 값이 없는 경우도 handling 가능하다.
'null'
```

## Example

```
>>> c
{'미나': ['twice1', 'leader'], '사나': ('twice', 'team')}
>>> c['미나'][0] = 'twice2'

>>> c
{'미나': ['twice2', 'leader'], '사나': ('twice', 'team')}

>>> c['사나'][0] = 'twice2'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>>

>>> '사나' in c.keys()
True

>>> 'twice' in c.values()
False

>>> 'twice2' in c.values()
False

>>> ['twice2','leader'] in c.values()
True
```

## Set

```
my_set = {1, 2, 3, 4}
my_set.add(5)  # 요소 추가
print(my_set)  # {1, 2, 3, 4, 5}

my_set.add(3)  # 중복된 값은 추가되지 않음
print(my_set)  # {1, 2, 3, 4, 5}
```

## Thread Local

```
import threading

# ThreadLocal과 같은 역할을 하는 객체 생성
thread_local_data = threading.local()

def process_data():
    # 각 스레드마다 독립적인 변수를 가질 수 있음
    print(f"Thread {threading.current_thread().name} has data: {thread_local_data.value}")

def worker(name):
    # 각 스레드가 독립적인 데이터를 저장
    thread_local_data.value = name
    process_data()

# 스레드 생성
thread1 = threading.Thread(target=worker, args=("Thread-1's data",), name="Thread-1")
thread2 = threading.Thread(target=worker, args=("Thread-2's data",), name="Thread-2")

# 스레드 실행
thread1.start()
thread2.start()

# 스레드가 끝날 때까지 기다림
thread1.join()
thread2.join()
```
