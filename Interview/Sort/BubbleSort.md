- Bubble Sort
	- 將 array 由小至大排序
	- 由前開始兩兩比較，若首元素較大則將其與後者對調，第一輪結束後，最後一個元素一定最大，再開始第二輪的比較
	- ![image](https://github.com/bebe6990103/LeetCode/blob/main/Image/bubble.png)
```cpp
#include <stdio.h>

void print_arr(int* arr, int size) {
    
    for(int i=0; i<size; i++)
    {
        printf("%d ", arr[i] );
    }
    
}
int main() {
    int numbers[] = {15, 80, 53, 4, 109};

    int i, j, temp;
    int n = sizeof(numbers)/sizeof(int);
    
    for( i=n-1; i>0; i--)
    {
        for( j=0; j<=i-1; j++)
        {
            if( numbers[j]>numbers[j+1] )
            {
                temp = numbers[j];
                numbers[j] = numbers[j+1];
                numbers[j+1] = temp;
            }
        }
    }

    print_arr(numbers, n);

    return 0;
}
```
