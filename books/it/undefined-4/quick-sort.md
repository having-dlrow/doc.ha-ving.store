# - 퀵정렬 (Quick Sort)

## Summary

* 오름차순정렬한다.
* 오른쪽/왼쪽분할, 정복
  * :thumbsup: 오른쪽 나눌 때, pivotal 값 보다 낮은 값들로 나뉜다.

## Code

```java
void quickSort(int[] arr, int low, int high){
    int left = partition(arr, low, high);

    quickSort(arr, low, left-1);
    quickSort(arr, left, high);
}

int partition(int[] arr, int low, int high){
    if(low >= high) return;
    
    int index = (low + high) / 2
    int pivot = arr[index];
    while(low <= high){
        while(arr[low] < pivot) low++;
        while(arr[high] > pivot) high--;
        if(low <= high){
            swap(arr, low, high);
            low++;
            high--;
            
            // 여기에 break 없이 pivot 보다 작은 값을 left로 가야함!
        }
    }

    return start;
}

void swap(int[] arr, int low, int high){
    int temp = arr[low];
    arr[low] = arr[high];
    arr[high] = temp;
}
```

## Example

```

// [5, 3, 8, 4, 9, 1, 6, 2, 7] func(arr,0,8) pivot(i):4 
[5, 3, 8, 4, *7, 1, 6, 2, *9]       left:4, right:8, pivot(value):9
└>
    // [5, 3, 8, 4, 7, 1, 6, 2] func(arr,0,7) pivot(i):3
    [*2, 3, 8, 4, 7, 1, 6, *5]      left:0, right:7, pivot(value):4
    [2, 3, *1, 4, 7, *8, 6, 5]      left:2, right:5, pivot(value):4
    [2, 3, 1, *4, 7, 8, 6, 5]       left:3, right:3, pivot(value):4
    └>
        // [2, 3, 1, 4]         func(arr,0,3) pivot(i):1
        [2, *1, *3, 4]              left:1, right:2, pivot(value):3
        └>
            // [2, 1]           func(arr,0,1) pivot(i):0
            [*1, *2]                left:0, right:1, pivot(value):2
            
            // [3, 4]           func(arr,2,3) pivot(i):2
            [3, 4]                  left:2, right:2, pivot(value)3
                
        // [7, 8, 6, 5]         func(arr,4,7) pivot(i):5  
        [7, *5, 6, *8]              left:5, right:7, pivot(value):8
        └>
            // [7, 5, 6]        func(arr,4,6), pivot(i):5
            [*5, *7, 6]             left:4, right:5, pivot(value):5
            └>     
                // [5]          func(arr,4,4), pivot(i):4
                // [7, 6]       func(arr,5,6), pivot(i):5                
                [*6, *7]             left:5, right:6, pivot(value):7
                
            // [5]              func(arr,7,7), pivot(i):7
// [9]                          func(arr,8,8), pivot(i):8
```

## 복잡도

* 최선 시간 복잡도 :  O(nlog₂n) &#x20;
  * 2^n 으로 깊이가 들어가므로
* 최악의 경우 : O(n^2)
* 공간 복잡도 : O(n)
