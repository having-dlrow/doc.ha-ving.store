# MVC 요청시, Thread 생성 될텐데, 어떻게 1개의 Controller가 생성 될까?

\[ 문제 ]

* Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

\[ 정답 ]

*   해설

    #### 답변

    * @Controller 어노테이션을 타고 들어가면 @Component라는 어노테이션이 붙어있음
    * 따라서 컨트롤러는 IoC 컨테이너에 등록되어 Spring Bean으로 관리됨
      * Spring의 빈 생성 전략의 기본은 싱글톤 패턴
      * 싱글톤으로 관리되는 빈은 상태정보를 갖지 않음
    * IoC 컨테이너에 Controller Bean은 싱글톤 전략에 의해 1개만 존재하고, Application이 init되는 시점에 초기화 됨
      * 그리고 실제 사용되는 시점에 의존성 주입을 통해서 사용됨
    * 요청시마다 새로 Bean을 생성해서 사용하는 것이 아닌, 이미 생성된 Bean을 가져다 쓰게됨으로써 여러개의 Thread에서 Controller를 사용해도 결론적으로 1개의 동일한 Controller
      * 만약 요청이 올때마다 새로운 컨트롤러가 생기길 바란다면, Bean Scope를 싱글톤이 아닌 request 등으로 설정하면 가능

    #### Controller의 저장 위치

    * Controller 객체 자체는 Heap에 생성되지만, 해당 Class의 정보는 Method Area(Static 영역)에 저장됨
      * 따라서 static 영역에 저장되기 때문에 모든 Thread가 접근 가능하며, 객체의 Binary Code를 공유할 수 있음
      *

참고자료 : [https://velog.io/@ejung803/Spring-Web-MVC에서-요청-마다-Thread가-생성되어-Controller를-통해-요청을-수행할텐데-어떻게-1개의-Controller만-생성될-수-있을까요](https://velog.io/@ejung803/Spring-Web-MVC%EC%97%90%EC%84%9C-%EC%9A%94%EC%B2%AD-%EB%A7%88%EB%8B%A4-Thread%EA%B0%80-%EC%83%9D%EC%84%B1%EB%90%98%EC%96%B4-Controller%EB%A5%BC-%ED%86%B5%ED%95%B4-%EC%9A%94%EC%B2%AD%EC%9D%84-%EC%88%98%ED%96%89%ED%95%A0%ED%85%90%EB%8D%B0-%EC%96%B4%EB%96%BB%EA%B2%8C-1%EA%B0%9C%EC%9D%98-Controller%EB%A7%8C-%EC%83%9D%EC%84%B1%EB%90%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94)
