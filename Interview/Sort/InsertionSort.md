- Insertion Sort
	- 將 array 由小至大排序
	- 將未排序的元素一個個插入到左側已排序好的適當位置
  - Time Complexity
    - O(n^2)
    - 但當資料「接近排序完成」時，速度接近 O(n)
  - Space Complexity
    - O(1)
```cpp
#include <stdio.h>

void print_arr(int* arr, int size) {
    
    for(int i=0; i<size; i++)
    {
        printf("%d ", arr[i] );
    }
    printf("\n");
}

void insertion_sort(int* arr, int size) {
    int i, j, key;
    
    // 從第 2 個元素開始（index 1），因為第 1 個元素（index 0）預設已排序
    for (i = 1; i < size; i++) {
        key = arr[i];      // 這是我們要「插入」的目標
        j = i - 1;         // j 指向已排序部分的最後一個位置

        /* 將 key 與左側已排序好的元素逐一比較。
           如果左邊的數字比 key 大，就把它往右移一格。
        */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j]; // 往右移位
            j = j - 1;
        }
        
        // 找到位置後，將 key 插入
        arr[j + 1] = key;
    }
}

int main() {
    int numbers[] = {15, 80, 53, 4, 109};
    int n = sizeof(numbers)/sizeof(int);

    printf("Original: ");
    print_arr(numbers, n);
    
    insertion_sort(numbers, n);

    printf("Stored: ");
    print_arr(numbers, n);

    return 0;
}
```
