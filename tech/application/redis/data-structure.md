# 1. Data Structure

<table><thead><tr><th width="162">제공 데이터</th><th></th></tr></thead><tbody><tr><td>List</td><td>Linked List,  Quick List</td></tr><tr><td>Sets</td><td>SKIP List, ZIP List</td></tr><tr><td>Hash</td><td>-</td></tr><tr><td>Stream</td><td>-</td></tr></tbody></table>

## List

* 입력된 순서대로 저장됩니다.
* value가 하나도 없으면 키는 삭제됩니다.
* 값(string)을 비교

## Sets

* 입력된 순서와 상관없이 저장되며, 중복되지 않습니다.
* Sorted Sets는 key 하나에 여러개의 score와 value로 구성됩니다.

## Hash

* key 하나에 여러개의 field와 value로 구성됩니다. ( RDB 테이블과 가장 비슷)

## Stream

* 로그 데이터를 처리하기 위해서 5.0에서 새로 도입된 데이터 타입입니다.
* 입력된 순서가 유지됩니다.
* ID(숫자)를 비교 ( List 보다 속도가 빠름 )
* 소비자를 지정해서 데이터를 읽을 수 있다.
  * 지정된 소비자가 데이터를 제대로 처리했는지 확인하는 방법을 제공
  * 만약, 제대로 처리하지 못했다면, 다른 소비자를 할당해서 처리하도록 하는 방법을 제공
