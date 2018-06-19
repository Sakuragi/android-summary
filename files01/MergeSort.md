# 归并排序
## 算法思想：
将待排序序列R[0...n-1]看成是n个长度为1的有序序列，将相邻的有序表成对归并，得到n/2个长度为2的有序表；将这些有序序列再次归并，得到n/4个长度为4的有序序列；如此反复进行下去，最后得到一个长度为n的有序序列。

## 工作原理：
第一步：申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
第二步：设定两个指针，最初位置分别为两个已经排序序列的起始位置
第三步：比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
重复步骤3直到某一指针超出序列尾
将另一序列剩下的所有元素直接复制到合并序列尾
  
## 复杂度：
平均时间复杂度为O(nlogn) 。空间复杂度为 O(n)

## 稳定性：
归并排序是稳定的。

## java实现：

```
import java.util.*;


public class GBSort {
	
	/*函数功能：合并表长为gap的俩个有序表*/
     public void Merge(int[] array, int low, int mid, int high) {
        int i = low; //当前待排序第一段序列的第一个元素的下标
        int j = mid + 1; // 当前待排序第二段序列的第一个元素的下标
         int k = 0; // k是临时存放合并序列数组的下标
         int[] array2 = new int[high - low + 1]; //数组的长度为第一第二序列长度之和
  
         //  扫描第一段和第二段序列，直到有一个扫描结束
         while (i <= mid && j <= high) {
             //判断第一段和第二段取出的数哪个更小，将其存入合并序列，并继续向下扫描
             if (array[i] <= array[j]) {
                array2[k] = array[i];
                 i++;
                 k++;
             } else {
                 array2[k] = array[j];
                 j++;
                 k++;
             }
         }
 
         //若第一段序列还没扫描完，将其全部复制到合并序列 
         while (i <= mid) {
             array2[k] = array[i];
             i++;
             k++;
         }
 
         //若第二段序列还没扫描完，将其全部复制到合并序列
         while (j <= high) {
             array2[k] = array[j];
             j++;
             k++;
         }
			//将合并序列复制到原始序列中
         for (k = 0, i = low; i <= high; i++, k++) {
             array[i] = array2[k];
         }
     }
 
	/*函数功能：改变表长gap的值，调用Merge（）函数合并表，使每个有序表的长度为gap*/
     public void MergePass(int[] array, int gap, int length) {
         int i = 0;
 
		// 归并gap长度的两个相邻子表
         for (i = 0; i + 2 * gap - 1 < length; i = i + 2 * gap) {
             Merge(array, i, i + gap - 1, i + 2 * gap - 1);
         }
 
		// 当余下两个子表，后者长度小于gap
        if (i + gap - 1 < length) {
             Merge(array, i, i + gap - 1, length - 1);
         }
     }
 
     public int[] sort(int[] list) {
         for (int gap = 1; gap < list.length; gap = 2 * gap) {                    //gap为子表的长度
             MergePass(list, gap, list.length);
             System.out.print("gap = " + gap + ":\t");
            this.printAll(list);
         }
         return list;
     }
 
     // 打印完整序列
     public void printAll(int[] list) {
         for (int value : list) {
             System.out.print(value + "\t");
         }
         System.out.println();
     }
 
     public static void main(String[] args) {
         int[] array = {
                 9, 1, 5, 3, 4, 2, 6, 8, 7,2,5,4,10
         };
 
         GBSort merge = new GBSort();
         System.out.print("before sort :\t\t");
         merge.printAll(array);
         merge.sort(array);
         System.out.print("after sort :\t\t");
        merge.printAll(array);
     }
 }
```


----------
