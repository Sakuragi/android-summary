# 一、冒泡排序：
## 算法实现过程：
1）首先，从第一个元素开始，比较该元素与该元素相邻的下一个元素的大小（即第一个元素与第二个元素的大小），如果该元素比较大则交换位置，否则不交换位置。
2）按照1的步骤不断重复的比较下一元素与其相邻元素之间的大小，直到第n-1个元素，第一趟比较结束。例如：接下去是第二个元素，重复 1 的步骤，比较其与其相邻下一元素大小（即第二个元素与第三个元素的大小），大则交换位置，否则不交换。
3）持续重复以上步骤，直到没有元素可以比较

## 复杂度：
时间复杂度：最好的情况下O(n),最坏为倒序情况下：O(n2),平均为O(n2)。

## 稳定性：
冒泡排序算法是稳定的。

## 冒泡排序java实现：

```
/*一共要比较arr.length-1趟：for(int i=0;i<arr.length-1;i++)
	每趟要比较arr.length-1-i次（i为当前趟数）：for(int j=0;j<arr.length-i-1;j++)*/
	public void mp(int arr[]){
		for(int i=0;i<arr.length-1;i++){
			for(int j=0;j<arr.length-i-1;j++){
				if(arr[j]>arr[j+1]){
					int temp;
					temp=arr[j];
					arr[j]=arr[j+1];
					arr[j+1]=temp;
				}
			}
		}
		
		for(int k=0;k<arr.length;k++){
			System.out.print(" "+arr[k]+" ");
		}
	}
```


----------

注：部分代码来源于网络

