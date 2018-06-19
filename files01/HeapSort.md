# 堆排序：
## 什么是堆：
堆是一颗完全二叉树。堆又分大顶堆跟小顶堆，**大顶堆即其任意一个非叶子结点都不小于其子节点，即key[i]>=key[2*i+1]&&key[i]>=key[2*i+2]**，如下图：
![大顶堆](http://img.blog.csdn.net/20161001175503626)

**小顶堆即其任意一个非叶子结点都不大于其子节点**，即满足**Key[i]<=key[2i+1]&&Key[i]<=key[2i+2]。**
如下图：

![小顶堆](http://img.blog.csdn.net/20161001180010225)


## 堆排序复杂度：
对于n个关键字序列，最坏情况下每个节点需比较log2(n)次，因此其最坏情况下时间复杂度为nlogn。

## 堆排序稳定性：
堆排序为不稳定排序，不适合记录较少的排序。


## 堆排序算法基本思想：
**以大顶堆为例：**
给定一个整形数组a[]={16,7,3,20,17,8,6,1}
![大顶堆](http://img.blog.csdn.net/20161001184135033)

**一、先将指定序列变为大顶堆，步骤如下：**
**1）**选择最后一个非叶子节点的父节点，从其开始，比较其与其左、右（如果存在）子结点的大小，如果子节点比父节点大，则交换位置。

![这里写图片描述](http://img.blog.csdn.net/20161002151755328)

**如上图，最后一个非叶子结点即7号结点，与其父节点3号结点，a[7] < a[3]所以不用交换。**

**2）**重复递增选择刚比较完的结点的相邻非叶结点直到根节点，比较其与其子结点以及子节点的子节点（若存在，如果子节点还存在子节点的话就一直递归下去，直到叶子结点）的大小，按大顶堆的结点大小规则，交换结点的值。

**选择3号结点的相邻前一结点，即二号结点**
![这里写图片描述](http://img.blog.csdn.net/20161001185336843)

**比较其与子节点的大小，并与最大的那个节点交换值。交换后如下图：**

![这里写图片描述](http://img.blog.csdn.net/20161002090809007)

**继续选择1号结点：**
![这里写图片描述](http://img.blog.csdn.net/20161002091030273)

**比较其与其子结点以及子节点的子节点（若存在，如果子节点还存在子节点的话就一直递归下去，直到叶子结点）的大小**

![这里写图片描述](http://img.blog.csdn.net/20161002091155149)

**先比较子节点与其的大小，并交换值，在比较子节点的子节点与子节点的大小**
![这里写图片描述](http://img.blog.csdn.net/20161002091406214)

**1比7小不需要交换**
![这里写图片描述](http://img.blog.csdn.net/20161002091536635)

**接下去选择1号前一相邻结点，即0号结点**

![这里写图片描述](http://img.blog.csdn.net/20161002091714213)

**比较其与其子结点以及子节点的子节点（若存在，如果子节点还存在子节点的话就一直递归下去，直到叶子结点）的大小，并交换**
![这里写图片描述](http://img.blog.csdn.net/20161002092506217)

**比较子节点与其子节点的子节点的大小即下图中①部分，交换值**

![这里写图片描述](http://img.blog.csdn.net/20161002151458609)

**再比较子节点的子节点的子节点与该节点的父节点的大小（上图②部分），即7号结点与3号结点的大小，1比7小，不需要交换。**

**接下去比较0号节点的左结点与其子结点，不需要交换**
![这里写图片描述](http://img.blog.csdn.net/20161002093158470)

**如此，无需序列就变成了大顶堆了。**

**二、对大顶堆进行排序：**
**步骤**
1）将根元素与最后一个未排元素进行交换
2）剔除最新一个交换的元素，将新生成的序列重新排成大顶堆。
3）重复以上步骤，直到成为有序序列。

**将根元素与最后一个未排元素进行交换：**
![这里写图片描述](http://img.blog.csdn.net/20161002094231053)

**排成大顶堆：**
![这里写图片描述](http://img.blog.csdn.net/20161002094437257)

**重复以上步骤：**
![这里写图片描述](http://img.blog.csdn.net/20161002094656805)

![这里写图片描述](http://img.blog.csdn.net/20161002094811931)

![这里写图片描述](http://img.blog.csdn.net/20161002094940572)

![这里写图片描述](http://img.blog.csdn.net/20161002095043197)

![这里写图片描述](http://img.blog.csdn.net/20161002095211432)

![这里写图片描述](http://img.blog.csdn.net/20161002095224155)

如此一来，堆排序便完成了。


## java实现代码：
父节点为i，左、右子节点分别可以用 2*i+1，2* i+2表示。

```
public class HeapSortTest {  
  
    public static void main(String[] args) {  
        int[] data5 = new int[] { 5, 3, 6, 2, 1, 9, 4, 8, 7 };  
        print(data5);  
        heapSort(data5);  
        System.out.println("排序后的数组：");  
        print(data5);  
    }  
  
    public static void swap(int[] data, int i, int j) {  
        if (i == j) {  
            return;  
        }  
        data[i] = data[i] + data[j];  
        data[j] = data[i] - data[j];  
        data[i] = data[i] - data[j];  
    }  
  
    public static void heapSort(int[] data) {  
        for (int i = 0; i < data.length; i++) {  
            createMaxdHeap(data, data.length - 1 - i);  
            swap(data, 0, data.length - 1 - i);  
            print(data);  
        }  
    }  
  
    public static void createMaxdHeap(int[] data, int lastIndex) {  
        for (int i = (lastIndex - 1) / 2; i >= 0; i--) {  
            // 保存当前正在判断的节点  
            int k = i;  
            // 若当前节点的子节点存在  
            while (2 * k + 1 <= lastIndex) {  
                // biggerIndex总是记录较大节点的值,先赋值为当前判断节点的左子节点  
                int biggerIndex = 2 * k + 1;  
                if (biggerIndex < lastIndex) {  
                    // 若右子节点存在，否则此时biggerIndex应该等于 lastIndex  
                    if (data[biggerIndex] < data[biggerIndex + 1]) {  
                        // 若右子节点值比左子节点值大，则biggerIndex记录的是右子节点的值  
                        biggerIndex++;  
                    }  
                }  
                if (data[k] < data[biggerIndex]) {  
                    // 若当前节点值比子节点最大值小，则交换2者得值，交换后将biggerIndex值赋值给k  
                    swap(data, k, biggerIndex);  
                    k = biggerIndex;  
                } else {  
                    break;  
                }  
            }  
        }  
    }  
  
    public static void print(int[] data) {  
        for (int i = 0; i < data.length; i++) {  
            System.out.print(data[i] + "\t");  
        }  
        System.out.println();  
    }  
  
}  
```
