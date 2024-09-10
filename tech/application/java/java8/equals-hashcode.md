# equals() , hashcode()

## 요약

**equals() 와 hashcode()**

* equals() 는 두 개의 객체가 동일한지 동일성을 비교하는 것입니다. 즉, 객체가 **같은 메모리 주소**인지 비교합니다.
* hashcode() 는 **객체의 메모리 주소에 대한 해시 코드**를 반환하는 메소드입니다.&#x20;

**equals() 를 오버라이딩해서 사용하는 이유**

* 같은 객체로 인식해야 하는 경우가 있는데 이런 경우\
  동등성을 가지도록 equals() 를 오버라이딩 해주어야합니다.

**equals() 를 오버라이드할 때 hashcode() 도 같이 오버라이드 하는 이유**

* hashMap, hashSet
* 해시 충돌로 인한 조회 성능 저하

## equals() 와 hashcode() 의 차이점

**equals() 메서드는 주소기반 비교를 하지 않으며, Object 클래스의 구현에 한정하여, 내용이나 값을 비교한다.** 단순히 == 연산을 통한, 참조비교를 수행하며 이때, 객체가 같은 메모리 주소를 참조하는지 확인 할 수 있다.



반면, hashcode()는 기본적으로 메모리 주소를 해시코드로 변환하여 준다.&#x20;

```
    @IntrinsicCandidate
    public native int hashCode();
```

native 키워드를 통해 C/C++로 구현된 메서드에 의해 JVM에 할당된 메모리 주소를 기반으로 생성된 해시코드가 반환된다. 메모리 주소는 객체마다 고유한 값이기 때문에 해시 코드도 고유한 값을 가지게 됩니다.



조금  더 생각해보자.

아래 코드는  Lombok이 생성하는 equals()이다.  이 코드 역시 주소 비교가 아닌 값  비교이다.

```
    public boolean equals(final Object o) {
        if (o == this) return true;                    // 주소 비교
        if (!(o instanceof Course)) return false;
        final Course other = (Course) o;
        if (!other.canEqual((Object) this)) return false;
        final Object this$title = this.getTitle();
        final Object other$title = other.getTitle();
        if (this$title == null ? other$title != null : !this$title.equals(other$title)) return false; // 값 비교
        return true;
    }

요약: 객체가 title 이라는 변수를 가지는 상황에서, instanceof을 통해 class를 비교하고, 변수의 값을 비교 하고 있다.
```

### Object.equals()

Object 기본 구현은 객체 메모리 주소 비교이다. Object.equals()는 두 객체가 같은 메모리 주소인 경우 true 반환한다.

```
    public boolean equals(Object obj) {
        return (this == obj);  // 참조 비교 (주소 비교)
    }
```

위 코드에서는 title이라는 String 타입에 대해 equals 수행한다.&#x20;

```
if (this$title == null ? other$title != null : !this$title.equals(other$title)) return false;
```

<mark style="color:red;">**Object와 String 객체 equals가 다르다는 것을 항상 기억하자.**</mark>&#x20;



\[참고] string.equals

```
// String.java
    public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        return (anObject instanceof String aString)
                && (!COMPACT_STRINGS || this.coder == aString.coder)
                && StringLatin1.equals(value, aString.value);
    }

// StringLatin1.java
    @IntrinsicCandidate
    public static boolean equals(byte[] value, byte[] other) {
        if (value.length == other.length) {
            for (int i = 0; i < value.length; i++) {
                if (value[i] != other[i]) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }
```

### instanceOf

클래스의 이름이나 주소를 직접 비교하지 않는다. 객체가 속한 클래스 타입을 런타임시 확인하여 비교한다.&#x20;

JVM이 객체의 실제 클래스 타입(타입 메타데이터)를 확인하는 방식이다.

```
class Animal {}
class Dog extends Animal {}

Animal animal = new Animal();
Dog dog = new Dog();

System.out.println(animal instanceof Animal); // true (Animal 타입이므로)
System.out.println(dog instanceof Dog);       // true (Dog 타입이므로)
System.out.println(dog instanceof Animal);    // true (Dog는 Animal의 하위 클래스이므로)
System.out.println(animal instanceof Dog);    // false (Animal은 Dog의 상위 클래스가 아님)
```



## equals() 는 오버라이드 해서 사용한 경험

객체의 메모리 주소가 아니라, 객체의 상태나 값이 같은지 비교를 원하는 경우,\
equals() 변경하여 사용 할 수 있다.



<mark style="color:blue;">**HashSet**</mark>, HashMap 같은 컬렉션에서 중복처리 하는 경우, equals 오버라이딩한 객체를 통해 정확한 중복체크가 가능하다.

```
Set<Person> personSet = new HashSet<>();
Person p1 = new Person("John", "123456");
Person p2 = new Person("Jane", "123456");

personSet.add(p1);
personSet.add(p2);

System.out.println(personSet.size()); // 1: 중복된 idNumber 때문에 중복 제거됨
```

주민 번호가 같으면, 동일한 사람으로 간주했을 때, 두 객체가 이름이 다르더라도 equlas() 따라 동일한 객체로 간주된다.

```
class Person {
    private String name;
    private String idNumber; // 주민번호 또는 고유 식별자

    public Person(String name, String idNumber) {
        this.name = name;
        this.idNumber = idNumber;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true; // 같은 객체라면 true
        if (!(o instanceof Person)) return false; // 타입이 다르면 false
        Person person = (Person) o;
        return idNumber.equals(person.idNumber); // 주민번호가 같으면 같은 사람으로 간주
    }

    @Override
    public int hashCode() {
        return idNumber.hashCode(); // equals()와 일관되게 idNumber로 해시 코드 생성
    }
}
```

\*HashMap 과정

1\) hashCode() 사용, 키 계산

2\) equals() 사용, 키가 같은 값인지 확인, 같은 해시코드를 가지는 다른 객체가 있을 수 있기 때문

## equals() 를 오버라이드 시, hashcode()도 오버라이드 하는 이유

1. 해시 기반 컬렉션, 중복 제거 불가

```
class Person {
    private String name;
    private String idNumber;

    public Person(String name, String idNumber) {
        this.name = name;
        this.idNumber = idNumber;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return idNumber.equals(person.idNumber);
    }

    @Override
    public int hashCode() {
        return super.hashCode(); // 기본 Object의 hashCode 사용 (메모리 주소 기반)
    }
}

public class Main {
    public static void main(String[] args) {
        HashSet<Person> set = new HashSet<>();

        Person p1 = new Person("John", "123456");
        Person p2 = new Person("Jane", "123456"); // 다른 객체지만 idNumber가 동일함

        set.add(p1);
        set.add(p2);

        System.out.println(set.size()); // 2, 논리적으로 같은 객체인데도 중복이 발생
    }
}
```

위 코드와 같이 equlas는 논리적으로 동일한 객체라고 하지만, hascode는 다른 객체라고 하는 경우, \
중복된 객체가 컬렉션에 저장되므로, HashMap, HashSet 사용 목적이 없다.



2.

```
class PersonB {
    private String name;
    private String idNumber;

    public PersonB(String name, String idNumber) {
        this.name = name;
        this.idNumber = idNumber;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof PersonB)) return false;
        PersonB person = (PersonB) o;
        return idNumber.equals(person.idNumber);
    }

    @Override
    public int hashCode() {
        return idNumber.hashCode(); // 해시 코드 중복 발생
    }
}

public class Main {
    public static void main(String[] args) {
        
        HashMap<PersonA, String> mapA = new HashMap<>();
        long startTimeA = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            PersonA p = new PersonA("Person" + i, i+"");
            mapA.put(p, "Value " + i);
        }
        long endTimeA = System.nanoTime();
        System.out.println("Map A size: " + mapA.size());
        System.out.println("perform A: " + (endTimeA - startTimeA) + " ns");

        
        HashMap<PersonB, String> mapB = new HashMap<>();
        long startTimeB = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            PersonB p1 = new PersonB("Person" + i, "123456");
            mapB.put(p1, "Value " + i);             
        }
        long endTimeB = System.nanoTime();
        System.out.println("Map B size: " + mapB.size());
        System.out.println("perform B: " + (endTimeB - startTimeB) + " ns");

        
        PersonA searchPersonA = new PersonA("Person999", "123456");
        long searchStartTimeA = System.nanoTime();
        mapA.get(searchPersonA); 
        long searchEndTimeA = System.nanoTime();
        System.out.println("A time: " + (searchEndTimeA - searchStartTimeA) + " ns");

        PersonB searchPersonB = new PersonB("Person999", "123456");
        long searchStartTimeB = System.nanoTime();
        mapB.get(searchPersonB); 
        long searchEndTimeB = System.nanoTime();
        System.out.println("B time: " + (searchEndTimeB - searchStartTimeB) + " ns");
    }
}
--------------------
Map A size: 1000
저장perform A: 202,159,961 ns 
Map B size: 1
저장perform B: 73,761,413 ns
조회A time: 8250 ns
조회B time: 20450 ns
```

PersonA의 경우,  메모리 주소 기반으로 해시 충돌이 발생 하지 않고, \
PersonB의 경우 모든 객체가 동일한 해시코드를 갖는 경우

저장 성능 :

* A : 각각 다른 버킷에 저장 되어 있으므로 -> 많은 메모리 소유
* B : equals()를   통해기존 항목을 덮어쓰움 -> 저장 시간 적게 소요됨

검색 성능 :&#x20;

* A : 해시 충돌 발생 X -> 버킷 검색 빠름 -> 버킷   내 검색 없음
* B : 같은 버킷 저장 -> 모든 객체 equals() 비교 -> 검색 느림

_**검색시, 해시충돌로 인해, 여러 객체를 비교 해야 하므로 검색 성능이 느려진다.**_



Ref \
\- [https://mangkyu.tistory.com/101](https://mangkyu.tistory.com/101)\
[https://f-lab.kr/insight/java-object-class-equals-hashcode?gad\_source=1\&gclid=Cj0KCQjwudexBhDKARIsAI-GWYUqQXMQVnzKUdVa1oW2B-\_upTBwOVqfoXAToeQL6YRBfhW6rxniYYYaApewEALw\_wcB](https://f-lab.kr/insight/java-object-class-equals-hashcode?gad\_source=1\&gclid=Cj0KCQjwudexBhDKARIsAI-GWYUqQXMQVnzKUdVa1oW2B-\_upTBwOVqfoXAToeQL6YRBfhW6rxniYYYaApewEALw\_wcB)
