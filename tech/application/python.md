# 🎁 Python

{% embed url="https://wikidocs.net/11" %}

| 데이터 구조                                           | 순서 유지 | 중복 허용  | 가변 |
| ------------------------------------------------ | ----- | ------ | -- |
| Tuple                                            | O     | O      | X  |
| <mark style="background-color:blue;">List</mark> | O     | O      | O  |
| Dictionary                                       | O     | 키 중복 X | O  |

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
