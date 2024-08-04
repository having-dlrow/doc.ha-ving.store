# Lambda

\[ 문제 ]

* Java 8 버전의 특징을 말하세요.
  * 실제 면접에서는 답변에 대한 손코딩도 요구했습니다.

\[ 정답 ]

*   해설

    * Lambda, Optional, Stream이 대표적으로 출시됨

    ```java
            List<Integer> numList = Arrays.asList(0, 1, 2);

            // 1. 반복문 - Iterator
            for(Integer num: numList) {
                System.out.println(num);
            }

            // 2. 람다 표현식
            numList.forEach(x -> System.out.println(x));
    ```

    ```java
            Car car = new Car();

            // 1. NullPointerException 발생
            // System.out.println(car.getPerson().getName());

            // 2. 옵셔널을 검사해서 없는 경우 사용자 이름 없음 출력
            System.out.println(Optional.of(car)
                    .map(Car::getPerson)
                    .map(Person::getName)
                    .orElse("사용자 이름 없음"));
    ```

    * interface 에 default 와 static 메소드를 사용할 수 있게됨
      * 기존의 인터페이스에서는 상수와 추상 메서드만을 가질 수 있었으나 default 키워드와 static 키워드를 사용하여 인터페이스의 메소드 구현부를 작성할 수 있게 되었습니다.
      * default 키워드가 추가된 이유 :[https://grandma-coding.tistory.com/entry/Java-Default-Methods디폴트-메소드](https://grandma-coding.tistory.com/entry/Java-Default-Methods%EB%94%94%ED%8F%B4%ED%8A%B8-%EB%A9%94%EC%86%8C%EB%93%9C)
