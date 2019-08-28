# leetcode_note

## 目录  
-[排序算法](#排序算法)      
-[数组](#数组)

# 排序算法    
![paixu.png](https://i.loli.net/2019/08/28/zhgjsnJRGc1meFq.png)
> **术语说明** <br>
稳定：如果a原本在b前面，而a=b，排序之后a仍然在b的前面； <br>
不稳定：如果a原本在b的前面，而a=b，排序之后a可能会出现在b的后面；  <br>
内排序：所有排序操作都在内存中完成；  <br>
外排序：由于数据太大，因此把数据放在磁盘中，而排序通过磁盘和内存的数据传输才能进行；  <br>
时间复杂度： 一个算法执行所耗费的时间。  <br>
空间复杂度：运行完一个程序所需内存的大小。 <br>
n: 数据规模<br>
k: “桶”的个数<br>
In-place: 占用常数内存，不占用额外内存<br>
Out-place: 占用额外内存<br>

**排序分类**
![分类.jpg](https://i.loli.net/2019/08/28/LlqpgvTi6OGnxBo.png)

# 插入排序      

插入排序：插入排序基本操作就是将一个数据插入到已经排好序的有序数据中，从而得到一个新的、个数加一的有序数据，算法适用于少量数据的排序，时间复杂度为O(n^2)。是稳定的排序方法。插入排序的基本思想是：每步将一个待排序的纪录，按其关键码值的大小插入前面已经排序的文件中适当位置上，直到全部插入完为止。
```java
/**
 * 插入排序
 * 直接插入排序：
 *  基本思想：
 *  在要排序的一组数中，假设前面(n-1)[n>=2] 个数已经是排
 *  好顺序的，现在要把第n个数插到前面的有序数中，使得这n个数
 *  也是排好顺序的。如此反复循环，直到全部排好顺序。
 *
 *  直接插入排序是由两层嵌套循环组成的。外层循环标识并决定待比较的数值。
 *  内层循环为待比较数值确定其最终位置。直接插入排序是将待比较的数值与它的前一个数值进行比较，
 *  所以外层循环是从第二个数值开始的。当前一数值比待比较数值大的情况下继续循环比较，
 *  直到找到比待比较数值小的并将待比较数值置入其后一位置，结束该次循环。
 *
 *  时间复杂度：O(n2)
 *  空间复杂度：O(1)
 *
 *  稳定性：稳定
 *
 */

public class Insert_Sort {
    public static void main(String[] args) {

        int arr[] = {1,4,6,8,2,5,3,7,9};
        System.out.println("数组排序前顺序：");
        for(int n : arr){
            System.out.print(n+" ");
        }

        //直接插入排序
        insertSort(arr);

        System.out.println("\n数组排序后顺序：");
        for(int n : arr){
            System.out.print(n+" ");
        }

    }

    //直接插入排序
    private static void insertSort(int[] arr){
        // {1,4,6,8,2,5,3,7,9}
        //{1,4,6,8,8,5,3,7,9}
        //外层循环确定待比较数值
        for (int i=1;i<arr.length;i++) {  //必须i=1，因为开始从第二个数与第一个数进行比较
            int temp = arr[i];  //待比较数值
            int j = i - 1;
            //内层循环为待比较数值确定其最终位置
            for (;j>=0 && arr[j]>temp;j--) {  //待比较数值比前一位置小，应插往前插一位
                //将大于temp的值整体后移一个单位   8>2
                arr[j+1] = arr[j];            
            }
            arr[j+1] = temp; //待比较数值比前一位置大，最终位置无误
        }
    }
}

```

```python
def insert_sort(arr):
    for i in range(1,len(arr)):
        cur = arr[i]
        j = i-1
        while j>=0 and arr[j] > cur:
            arr[j+1] = arr[j]
            j -=1
        arr[j+1] = cur

if __name__ == '__main__':
    arr = [1,5,8,6,9,7,23,7,8,3]
    #  1, 3, 4, 8, 5 
                j  i 
    #  1, 3, 4, 8, 8


    print (arr)
    insert_sort(arr)
    print (arr)

'''举例
第一步  1,3,4,8,5
            j,i
            j = 3; i = 4 ; cur = arr[i] = 5
第二步  arr[j] = 8 > arr[i] =5 
 所以把 5的位置赋值为8 得到
       1,3,4,8,8
 同时 j-1 = 2

第三步  此时 arr[j] = 4 < 5 不进入while循环
 所以把 arr[j+1] = arr[3] = 8 的位置复制为cur 也就是5
 得到  1,3,4,5,8

'''
```




## 快排
**快速排序**：
快速排序（Quicksort）是对冒泡排序的一种改进。它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。
```java
// 快排
package algrithm;
import java.util.Arrays;
public class QuickSort {
    public static void main(String[] args) {
        int[]  arr = new int[] {5,6,2,21,5,23,5,6,7,9,2,1,1};
        quickSort(arr, 0 , arr.length-1);
        System.out.println(Arrays.toString(arr));
    }
    public static void quickSort( int[] arr, int start, int end){
        if(start < end){
            //把数组中的第0个数作为标准数
            int stard = arr[start];
            // 记录需要排序的下标
            int low = start;
            int high = end;
            //循环找比标准数大的数和比标准数小的数
            while(low <high){
                //如果high大于stard数，则high--;
                while(low<high && arr[high] >= stard){
                    high--;
                }
                arr[low] = arr[high];
                //如果左边的数比stard数小
                while(low < high && arr[low]<stard){
                    low++;
                }
                arr[high] = arr[low];
            }
            // 把标准数赋值给低位置所在的元素
            arr[low] = stard;
            // 递归较小的数组
            quickSort(arr, start, low);
            // 递归教大的数组
            quickSort(arr,low+1, end);
        }
}
}

```

```python
arr = [1,5,6,1,7,23,7,8,3]

def quick_sort(arr, start,end ):
    if start >= end:
        return
    low = start
    high = end
    mid = arr[low]

    while low < high and arr[high] > mid:
        high-=1
    arr[low] = arr[high]
    while low < high and arr[low] < mid:
        low +=1
    arr[high] = arr[low]
    
    arr[low] = mid
    quick_sort(arr,0, low)
    quick_sort(arr, low+1 ,end)



if __name__ == '__main__':
    print (arr)
    quick_sort(arr,0,len(arr) -1)
    print (arr) 

```

# 数组
[01._two_sum](https://xiao7462.github.io/2019/02/10/Two-Sum/)                     
[02._add_two_numbers](https://xiao7462.github.io/2019/03/26/2.-Add-Two-Numbers)           
[27. Remove Element](https://xiao7462.github.io/2019/04/01/27.-Remove-Element/)     
