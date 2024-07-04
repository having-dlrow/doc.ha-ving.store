# @Transient

```
@Entity
public class Member{
    @Id
    private Long id;
    private String userId;
    private String password;
    private String confirmPassword;
    
    @Transient
    public String getComfirmPassword(){ return this.confirmPassword; }
}
```

예시 처럼, DB 테이블 컬럼으로 매핑하지 않는 항목 ( ConfirmPassword ) 에 사용한다. (= 영속 대상 제외 )



## @Transient 이해가기

```
@Target({ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface Transient {}
```

### FIELD 에 적용한 모습

```
Hibernate: 
    create table product (
       id bigint not null,
       name varchar(255),
       price decimal(19,2),
       primary key (id)
    )
```

### Method에 적용한 모습

(주의) Getter 메서드에 애노테이션 선언해야한다.

```
Hibernate: 
    create table member (
       id bigint not null,
       user_id varchar(255),
       password varchar(255),
       confirm_password varchar(255), <-- 하지만 영속 대상에서 제외되지 않음
       primary key (id)
    )
```



## 의도와 다르게 된 이유가 뭘까?

### JPA가 엔티티 객체에 접근하는 방식

**@Id 가 필드방식이면, 나머지 항목도 필드 방식으로 읽는다.**\
**@Id 가 프로퍼티 방식이면, 나머지항목도 프로퍼티 방식으로 읽는다.**

따라서 위 예시에서는 @Id가 필드 방식이므로,  프로퍼티 방식이 인식되지 않아, confirmPassword가 영속대상에서 제외되지 않았다.

<details>

<summary>프로퍼티 방식</summary>

```
@Entity
public class Member{
    @Id
    private Long id;
    private String name;
    ...
}
```

</details>

<details>

<summary>필드 방식</summary>

```
@Entity
public class Member{
    private Long id;
    private String name;
    
    @Id
    public Long getId(){return this.id;}
    public void setId(Long id){this.id = id;}
    
    public String getName(){return this.name;}
    public void setName(String name){this.name = name;}
}
```

</details>



ps. 컬럼 매핑 레퍼런스 애노테이션 : @Column, @Enumerate, @Temporal, <mark style="color:orange;">@Transient</mark>

* @Column : 컬럼을 매핑한다.
* @Enumerated : enum 타입을 매핑한다.
* @Temporal : 날짜 타입 매핑한다.
* <mark style="color:orange;">@Transient</mark> : 해당 필드를 테이블 컬럼과 매핑 시키지 않는다.
* @Access : JPA가 엔티티 접근하는 방식을 지정한다.

\
