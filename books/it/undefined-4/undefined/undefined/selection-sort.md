# - 선택 정렬 (Selection Sort)

## Summary

* 앞부터 맞춘다.
* 최소값을 찾는다. 해당값과 swap 한다.

## Code

```java
void selectionSort(int[] arr) {
    int temp;
    for( int i =0; i < arr.length; i++ ) {
        int position = i;
        // 최소값을 찾는다.
        for( int j= i+1; j < arr.length; j++ ) {
            if( arr[position] > arr[j]) {
                position = j;
            }
        }
        
        // 변경한다.
        temp = arr[i];
        arr[i] = arr[position];
        arr[position] = arr[i];
    }
}
```



복잡도&#x20;

* 시간복잡도 **O(n^2)**&#x20;
* 공간복잡도 **O(n)**&#x20;
