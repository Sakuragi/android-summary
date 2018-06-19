# 快速排序：
## 算法思想:
 思想：找一个记录，以它的关键字作为“枢轴”，凡其关键字小于枢轴的记录均移动至该记录之前，反之，凡关键字大于枢轴的记录均移动至该记录之后。致使一趟排序之后，记录的无序序列 R[s..t]将分割成两部分：R[s..i-1]和R[i+1..t],
且 R[j].key≤ R[i].key ≤ R[j].key (s≤j≤i-1) 枢轴(i+1≤j≤t)。
 例如:关键字序列
52, 49, 80, 36, 14, 58, 61, 97, 23, 75
调整为: 23, 49, 14, 36, (52) 58, 61, 97, 80, 75 

其中(52)为枢轴，在调整过程中，需设立两个指针:low 和 high，它们的初值分别为:s 和 t, 之后逐渐减小 high，增加 low，并保R[high].key≥52，R[low].key≤52,否则进行记录的“交换”。 在对无序序列中记录进行了一次分割之后，分别对分割所得的两个子序列进行快速排序，依次类推，直至每个子序列中只含一个记录为止。 


动画演示可以查看：
http://www.tyut.edu.cn/kecheng1/site01/suanfayanshi/quick_sort.asp


## java代码实现

```
public class quick {
 4     public void quick_sort(int[] arrays, int lenght) {
 5         if (null == arrays || lenght < 1) {
 6             System.out.println("input error!");
 7             return;
 8         }
 9         _quick_sort(arrays, 0, lenght - 1);
10     }
11 
12     public void _quick_sort(int[] arrays, int start, int end) {
13         if(start>=end){
14             return;
15         }
16         
17         int i = start;
18         int j = end;
19         int value = arrays[i];
20         boolean flag = true;
21         while (i != j) {
22             if (flag) {
23                 if (value > arrays[j]) {
24                     swap(arrays, i, j);
25                     flag=false;
26 
27                 } else {
28                     j--;
29                 }
30             }else{
31                 if(value<=arrays[i]){
32                     swap(arrays, i, j);
33                     flag=true;
34                 }else{
35                     i++;
36                 }
37             }
38         }
39         snp(arrays);
40         _quick_sort(arrays, start, j-1);
41         _quick_sort(arrays, i+1, end);
42         
43     }
44 
45     public void snp(int[] arrays) {
46         for (int i = 0; i < arrays.length; i++) {
47             System.out.print(arrays[i] + " ");
48         }
49         System.out.println();
50     }
51 
52     private void swap(int[] arrays, int i, int j) {
53         int temp;
54         temp = arrays[i];
55         arrays[i] = arrays[j];
56         arrays[j] = temp;
57     }
58 
59     public static void main(String args[]) {
60         quick q = new quick();
61         int[] a = { 49, 38, 65,12,45,5 };
62         q.quick_sort(a,6);
63     } 
64 
65 }
```
