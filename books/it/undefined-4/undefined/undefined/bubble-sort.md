# - 거품 정렬 (Bubble Sort)

## Summary

* 최대 값을 뒤로 이동한다.
* 앞뒤 비교, 뒤부터 맞춘다.

## Code

```java
void bubbleSort(int[] arr) {

    int temp =0
    for(int i =0; i <arr.length; i++) {
        // 뒤 부터 맞추므로, 한개씩 끝까지 가지 않아도 됨
        for(int j =1; j <arr.length-i; j++) {
            if(arr[j-1] > arr[j]) {
                temp = arr[j-1];
                arr[j-1] = arr[j]; 
                arr[j] = temp;
            }
        }
    }
}
```

## 복잡도

* 최선 시간 복잡도 **O(n^2)**&#x20;
* 최악 시간 복잡도 **O(n^2)**&#x20;
* 공간 복잡도 **O(1)**&#x20;
