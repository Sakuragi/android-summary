# 直接选择排序：

## 算法原理：

直接选择排序(Straight Select Sorting) 也是一种简单的排序方法，它的基本思想是：第一次从R[0]~R[n-1]中选取最小值，与R[0]交换，第二次从R[1]~R[n-1]中选取最小值，与R[1]交换，….，第i次从R[i-1]~R[n-1]中选取最小值，与R[i-1]交换，…..，第n-1次从R[n-2]~R[n-1]中选取最小值，与R[n-2]交换，总共通过n-1次，得到一个按排序码从小到大排列的有序序列·

##稳定性与复杂度：

选择排序不是一个稳定的排序算法，元素容易发生位置的变化。如序列5 8 5 2 9，我们知道第一遍选择第1个元素5会和2交换，那么原序列中2个5的相对前后顺序就被破坏了。 
时间复杂度是O(n^2)。

## java实现：

    public void zjxzsort(int[] arr){
        for(int i=0;i<arr.length-1;i++){
            int smalllestIndex=i;
            int min=arr[i];
            for(int j=i+1;j<arr.length;j++){
                if(arr[j]<min){
                    min=arr[j];
                    smalllestIndex=j;
                }
            }
            arr[smalllestIndex]=arr[i];
            arr[i]=min;

        }
    }

