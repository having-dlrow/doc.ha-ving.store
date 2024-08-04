# ≤ JAVA8

## Wrapper Class

### int\[] -> Integer\[]

```java
Integer[] asList = Arrays.steram(int_array)
                          .boxed()
                          .toArray(Integer[]::new);
```

### int\[] -> List\<Integer>

#### 🆖 Primitive -> Wrapper 로 변환 할 수 없다

```java
/* for 또는 stream 으로 가능 */
int[] int_array = new int[] {1,2,3,4,5};

// stream 방법
Arrays.stream(int_array)
       // Primitive -> Wrapper
       .boxed()
       // List
       .collect(Collectors.toList()); 
/* -----------------
 * asList[0] = 1;
 * asList[1] = 2;
 * asList[2] = 3;
 * asList[3] = 4;
 * asList[4] = 5;
 */
```

잘못 변환 되는 케이스 1 )

```java
  Arrays.asList(int_array); 
  /* -----------------
  * asList[0] = {1,2,3,4,5} 
  */
```

### List\<Integer> -> int\[]

#### 🆖 List\<int> 타입은 저장되지 않는다. Collection에 Primitive 타입이 허용되지 않는다.

```java

List<Integer> asList;
int[] int_array = asList
                    .stream()
                    .mapToInt(Integer::intValue)
                    .toArray();
/* -----------------
 * new int[] {0, 1, 2, 3, 4, 5} 
 */
```

