# leetcode_note

#目录  
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
arr = [1,5,6,1,7,23,7,8,3,]

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
