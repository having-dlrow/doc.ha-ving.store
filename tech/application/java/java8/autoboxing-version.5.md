# autoboxing ( version.5 )

* upcasting
  * 하위 클래스의 객체를 상위 클래스 타입으로 변환
* downcasting
  * 상위 클래스 타입의 객체를 하위 클래스 타입으로 변환

Boxing

* Primitive Type → Object Wrapper Class 전환

UnBoxing

* Object Wrapper Class → Primitive Type

목적

* JAVA5에서 Collection 같은 객체 기반 데이터 구조에 Primitive Type 저장이 불가 하다.
* 이전 Primitive Type 과 Object 사용으로 인한 수작업 및 혼돈을 줄여, 간결하다.

int

* Primitive Type 이다.
* 지역 변수로 선언된다면, JVM Stack에 저장된다.

Integer

* Object Wrapper Class 이다.
* 객체로, JVM Heap에 저장된다.

Stream 코드

```jsx
int[] int_array = new int[] {1,2,3,4,5};

Arrays.stream(int_array)
       .boxed().toArray(Integer[]:new); // Integer[] array = new Integer[]{1,2,3,4,5}
```
