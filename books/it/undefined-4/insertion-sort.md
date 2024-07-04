# - 삽입정렬 (Insertion Sort)

## Summary

* 최소값을 찾고, 최소값 자리를 제외 및 저장하고
* 그 자리부터 뒤로 한칸씩 밀기

Code

```java
void insertionSort(int[] arr) {
    for( int i =1; i< arr.length; i++ ) {
        prev = i-1    
        // 값을 찾는다.
        temp = arr[i]
        while((prev >= 0) && arr[prev] > temp ) { ---> 찾고
            arr[prev+1] = arr[prev]               <--- 밀면서 돌아가기
            prev--;
        }
        arr[prev+1] = temp;
    }
}
```

## 복잡도

* 최선의 경우 **O(n)**&#x20;
* 최악의 경우 **O(n^2)**
* **공간 복잡도 O(n)**

## **선택정렬과 차이**

* 선택정렬 : index가 선택된 곳의 값을 찾는 방식&#x20;
* 삽입정렬 : 위치는  정해져 있지 않고, 조건을 만날때까지 한칸씩 민다.
