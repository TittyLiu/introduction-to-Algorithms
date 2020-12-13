<h2>Quick Sort(快速排序)</h2>

> 思想：基于**分而治之**策略的快速排序

1. **分而治之**策略在快速排序中的应用

   - 从输出数组中**随机选择**一个元素

     - 一般实践过程中，都是选择输入数组的**最后一个元素**

   - 被选择的元素称为**pivot element**

   - 把输入数组划分为两部分，划分规则如下：

     - 左半部分只包括小于等于**piovt element**的值( <= **piovt element**)

     - 右半部分只包括大于**piovt element**的值(> **piovt element**)

       **注意**:**piovt element**不包括在这两部分中</br>

   - 对划分的两部分数组分别进行排序

     - 排序你可以用任意高效的算法，我们选择使用冒泡算法

   - 最后，我们把已经有序的两个部分加速**piovt element**连接起来，获取一个有序的数组

2. Example

   - input array

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick01.gif)

   -   选择一个**pivot element(我们选择数组最后一个元素)**

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick02.gif)

   - 把数组划分基于**pivot element元素**划为左右两部分

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick003.gif)

   - 把左右两部分子数组分别进行排序

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick04.gif)   

   - 把有序的左右两部分加上**piovt element**进行连接

     ![](/Users/liulei/GitRepository/staticResource/images/sortImages/quick05.gif)

3. 简单易懂的快速排序算法

   - 首先，给出快速排序的伪代码

     ```
     QuickSort( double[] a )
        {
           if ( a.length ≤ 1 )
              return;    // Don't need sorting             
     
           Select a pivot;  // It's usually the last elem in a[]      
     
           Partition a[] in 2 halves:
              left[]: elements ≤ pivot
     	 right[]: elements > pivot;
     
           Sort left[];
           Sort right[];
     
           Concatenate: left[] pivot right[]
        }
     ```

   - Java 代码

     ```
     public static void sort( double[] a )
        {
           double[] left = null, right = null;
           int      nleft, nright; // 左半部分和右半部分的长度
           double   pivot;  
           int      i, j, k;
     
     
           if ( a.length <= 1 )
           {
            	 // 数组只有一个元素时
     	       return;
           }
     
     /* ========================================================
     	               选择"pivot"
     ======================================================== */
           pivot = a[a.length-1];   // 我们现在先选择最后一个元素作为piovt element
                                   
     
     
     /* ========================================================
     	    找到多少元素 <= 和 >(大于或者小于等于) piovt
      ======================================================== */
           nleft = nright = 0;
           for ( i = 0; i < a.length-1; i++ )
     	 if ( a[i] <= pivot )
                 nleft++;
     	 else
                 nright++;
     
     /* =================================================
             新建一个左子数组、右子数组
     ================================================= */
           left  = new double[nleft];
           right = new double[nright];
     
      /* =================================================
     	 把数组元素划分为2个子数组:
     
                  所有小于等于（<=）pivot放到左子数组 left[ ] 中
                  所有大于（>）pivot放到右子数组 right[ ] 中
      ================================================= */
           i = 0;
           j = 0;
           for ( k = 0; k < a.length-1; k++ )
     	        if ( a[k] <= pivot )
                 left[i++] = a[k];
     	        else
                 right[j++] = a[k];
     
      /* =================================================
     	     对左子数组和右子数组分别进行排序(调用冒泡排序算法)
       ================================================= */
           BubbleSort.sort(left);
           BubbleSort.sort(right);
     
      /* =================================================
            	 最后，对排序完数组和piovt element进行连接
     	================================================= */             
           k = 0;
     
           for ( i = 0; i < left.length; i++ )
              a[k++] = left[i];
     
           a[k++] = pivot;
     
           for ( j = 0; j < right.length; j++ )
              a[k++] = right[j];
        }
     ```

4. 思考一个问题：我们可以在冒泡排序处使用快速排序吗？

   - 思考

     - 快速排序算法也能够用于排序一个数组

     - 既然这样的话，那还等什么，赶紧把冒泡排序用快速排序替换吧

       ```
        /* =================================================
       	     对左子数组和右子数组分别进行排序(调用冒泡排序算法)
         ================================================= */
             BubbleSort.sort(left);
             BubbleSort.sort(right);
       ```

     - 替换之后

       ```
        /* =================================================
       	     对左子数组和右子数组分别进行排序(递归地调用自己)
         ================================================= */
             QuickSort.sort(left);
             QuickSort.sort(right)
       ```

   - 替换后的简单的快速排序代码：

     ```
        public static void sort( double[] a )
        {
           double[] left = null, right = null;
           int      nleft, nright; // Length of left[] and right[
           double   pivot;
           int      i, j, k;
     
     
           if ( a.length <= 1 )
           {
            	 // Array of 1 element is sorted....
     
     	 return;
           }
     
      /* ========================================================
     	               选择"pivot"
     	======================================================== */
           pivot = a[a.length-1];   // Use last element as pivot
                                    // This is the default choice...
     
     
      /* ========================================================
     	    找到多少元素 <= 和 >(大于或者小于等于) piovt
       ======================================================== */
           nleft = nright = 0;
           for ( i = 0; i < a.length-1; i++ )
     	 if ( a[i] <= pivot )
                 nleft++;
     	 else
                 nright++;
     
        /* =================================================
             新建一个左子数组、右子数组
     	 ================================================= */
           left  = new double[nleft];
           right = new double[nright];
     
       /* =================================================
     	 把数组元素划分为2个子数组:
     
                  所有小于等于（<=）pivot放到左子数组 left[ ] 中
                  所有大于（>）pivot放到右子数组 right[ ] 中
     	 ================================================= */
           i = 0;
           j = 0;
           for ( k = 0; k < a.length-1; k++ )
     	 if ( a[k] <= pivot )
                 left[i++] = a[k];
     	 else
                 right[j++] = a[k];
     
       /* =================================================
     	     对左子数组和右子数组分别进行排序(递归地调用自己)
        ================================================= */
           sort(left);    // Use Quick Sort   
           sort(right);   // Use Quick Sort    
     
        /* =================================================
            	 最后，对排序完数组和piovt element进行连接
     	  ================================================= */             
           k = 0;
     
           for ( i = 0; i < left.length; i++ )
                 a[k++] = left[i];
     
           a[k++] = pivot;
     
           for ( j = 0; j < right.length; j++ )
                 a[k++] = right[j];
        }
     ```

   - 接下来，我们通过下面的步骤看看快速排序是如何工作的：

     - Input array

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick06.gif)

     - 选择一个**piovt element** 我们暂时先选择数组最后一个元素

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick07.gif)

     - 基于**piovt element**划分数组为左子数组、右子数组两部分   

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick08.gif)

     - 对划分的左、右子数组分别调用快速排序进行排序 

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick09.gif)        

     - 为了方便演示，下面只展示左子数组的排序（因为右子数组的递归调用的深度更多）

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick10.gif)    

         

       > 注意：因为当前输入数组只有一个元素了，快速排序将会返回输入数组</br>

       

     -  每一部分的快速排序将会选择自己**piovt element**并且对数组进行划分

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick11.gif)                

     -  最后左子数组将会对有序的数组和**piovt element**进行连接，并返回有序的左子数组         

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick12.gif)

     - 右半部分数组将会做相同的工作，但是由于空间关系，我们省略掉右子数组的演示

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick13.gif)

     - 最终，第一次的递归调用将会连接已经排好序的左、右子数组和**piovt element**

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quick14.gif)

     - 看完了算法的演示图，我们现在打印快速排序的过程

       ```
       Before sort:  [6.4, 3.5, 9.2, 1.1, 8.9, 2.5, 7.5, 4.2]
       
              Input = [6.4, 3.5, 9.2, 1.1, 8.9, 2.5, 7.5, 4.2]
              Pivot = 4.2
              Left array  = [3.5, 1.1, 2.5]
              Right array = [6.4, 9.2, 8.9, 7.5]
                     Input = [3.5, 1.1, 2.5]
                     Pivot = 2.5
                     Left array  = [1.1]
                     Right array = [3.5]
                            Input = [1.1]
                            Done.
                            Input = [3.5]
                            Done.
                     Sorted Left array  = [1.1]
                     Sorted Right array = [3.5]
                     Concatented pieces = [1.1, 2.5, 3.5]
                     Input = [6.4, 9.2, 8.9, 7.5]
                     Pivot = 7.5
                     Left array  = [6.4]
                     Right array = [9.2, 8.9]
                            Input = [6.4]
                            Done.
                            Input = [9.2, 8.9]
                            Pivot = 8.9
                            Left array  = null
                            Right array = [9.2]
                                   Input = [9.2]
                                   Done.
                            Sorted Left array  = null
                            Sorted Right array = [9.2]
                            Concatented pieces = [8.9, 9.2]
                     Sorted Left array  = [6.4]
                     Sorted Right array = [8.9, 9.2]
                     Concatented pieces = [6.4, 7.5, 8.9, 9.2]
              Sorted Left array  = [1.1, 2.5, 3.5]
              Sorted Right array = [6.4, 7.5, 8.9, 9.2]
              Concatented pieces = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
       
       After sort:   [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
       ```

5. 原地排序的快速排序算法（我们平时生活中真正使用的算法）

   - 上面的快速排序算法有助于我们理解算法工作流程，但是效率却并不高     

     - 现在我们开始用伪代码整理一下快速排序思路

       ```
       QuickSort( double[] a )
          {
             if ( a.length ≤ 1 )
                return;    // 长度小于1，不需要排序             
       
             Select a pivot;  //选择一个元素作为数组分割的界限
       
             分割数组 a[] 为左右两部分:
                left[]: 左半部分所有的元素都小于 等于  pivot
       	       right[]: 右半部分所有的元素都 大于 pivot;
       
             Sort left[];
             Sort right[];
       
             连接: left[] pivot right[]
          }
       ```

     - 在上面的简化版的中

     - ```
       我们新建了两个数组 lefr[] 和 right[](这两个数组包含原始数组的一部分元素)
             
       接着，我们吧这俩个数组用其他排序方法进行排序
             
       ```

   - 通过对分割数组效率会更高

     - 更好的方式是通过传递子数组去排序

       ```
       1、使用原始数组，这样的话可以减少拷贝带来的时间和空间开销
       
       2、通过传递数组时，指定数组的排序范围，即传递范围形参给函数，比如
       
        sort( a, from, to )    意思是:
       
              只排序从from到to的范围内的元素 
              
              a[from], a[from+1], ..... , a[to-1]
       ```

     - 就地快速排序

       ```
       1、快速排序算法只对输入的数组进行排序
       
       2、因此，其被称为：就地快速排序
       ```

6. 就地快速排序算法的步骤

   - 一开始，我们先使用伪代码

     ```
     QuickSort( double[] a )
        {
           if ( a.length ≤ 1 )
              return;    // 长度小于1，不需要排序             
     
           Select a pivot;  //选择一个元素作为数组分割的界限
     
           分割数组 a[] 为左右两部分:
              left[]: 左半部分所有的元素都小于 等于  pivot
     	       right[]: 右半部分所有的元素都 大于 pivot;
     
           Sort left[];
           Sort right[];
     
           连接: left[] pivot right[]
        }
     ```

   - 唯一的区别在于

     ```
     在排序过程中，我们每一次排序的对象是原始数组（这意味着我们所有的操作都是在原始数组上进行，即原地操作）
     ```

   - Java 代码

     ```
     /* ========================================================
             Sort:  a[iLeft] a[iLeft+1] .... a[iRight-1]
     	======================================================== */
     
          void  QuickSort( double[] a, int iLeft, int iRight )
          {
             if ( iRight - iLeft ≤ 1 )
     	{
     	   // 数组长度为空或者为1的数组不需要排序，直接return
     	   return;
             }
     
             k = partition( a, iLeft, iRight );
                    // 返回分完区后的piviot的位置的数组
     
     	QuickSort( a, iLeft, k );   // 对分完区后的左半部分进行排序
     	QucikSort( a, k+1, iRight); // 对分完区后的右半部分进行排序
     
             // 现在连接操作已经不需要啦 !!!
             // 不需要再连接两个有序的数组，因为排序操作在数组内部进行!!!
          }
     ```

   - **Note：** 调用分区函数partition(a,left,right) 如下列调用所示：

     ```
     1、调用函数 partition(a, iLeft, iRight) 将会对下列数组元素进行票分区:
               a[iLeft] a[iLeft+1]  ..... a[iRight-1]     
        
        通过选择 pivot = a[iRight - 1],然后将数组划分为两部分：
             a、左半部分所有元素都小于等于 pivot
             b、右半部分所有元素都大于 pivot
             
      2、partition()函数必须使用原始数组
     ```

       Example 1

     ​            ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition01.gif)   

   ​         Example 2

   ​        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition02.gif)

      

   - 现在我们一起来看下原地排序的算法操作

     - Input array：

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick10.gif)

     -   为了对数组排序，我们调用QuickSort(a,0,8) **注意，我们的iRight是8**

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick11.gif)

     - QuickSort(a, 0 ,8)将会首先分割数组

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick12.gif)

     ​       **Notice: partition函数将会改变输入数组**

     - 当partition( a , 0 , 8)函数执行完毕后，函数返回索引 3（**即pivot的位置**）

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick12a.gif)

     ​        **Notice: 现在输入数组已经原地改变啦！！！**

     -  QuickSort(a , 0 , 8) 将会调用QuickSort(a , 0 ,3) 去对left() 数组进行排序

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick13.gif)

     -   QuickSort(a, 0 ,3)首先对数组进行分割

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick14.gif)            

     ​      Partition(a ,0 ,3)将会返回 索引**1（即pivot的位置）**

     - QuickSort(a, 0 ,3)将会调用**QuickSort(a, 0 ,1)**对左边的子数组进行排序

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick15.gif)

       因为数组只用一个元素，QuickSort(a , 0 , 1)将会立刻返回

     - QuickSort(a , 0 ,3)下一步将会调用**QuickSort(a ,2(=k+1), 3 )**对右边的子数组进行排序

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick16.gif)

        因为数组只有一个元素，**QuickSort(a, 2, 3)**将会立刻返回

     - 执行到这一步，程序将返回到**QuickSort(a ,0 , 3)**, 因为其方法已经执行完毕！！！

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick17.gif)

     - 我们返回到**QuickSort(a , 0 ,8)**, 此时，输入数组看起来像这样

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick18.gif)

       此时，**QuickSort(a , 0 ,8)**将会调用 **QuickSort(a, 4(=k+1), 8)**对右子数组进行排序

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/quick19.gif)

     - 程序将会循环的对右子数组进行排序（此处就省略........）

   - 下面打印出来，原地排序算法的实际执行过程

     ```
     Before sort:  [6.4, 2.5, 9.2, 3.5, 8.9, 1.1, 7.5, 4.2]
     
            **QuickSort(a, 0, 8)**
            Input: [6.4, 2.5, 9.2, 3.5, 8.9, 1.1, 7.5, 4.2]
            a[] = [6.4, 2.5, 9.2, 3.5, 8.9, 1.1, 7.5, 4.2]
            Pivot = 4.2
            After partition: [1.1, 3.5, 2.5, 4.2, 9.2, 8.9, 6.4, 7.5]
                   **QuickSort(a, 0, 3)**
                   Input: [1.1, 3.5, 2.5]
                   a[] =  [1.1, 3.5, 2.5, 4.2, 9.2, 8.9, 6.4, 7.5]
                   Pivot = 2.5
                   After partition: [1.1, 2.5, 3.5, 4.2, 9.2, 8.9, 6.4, 7.5]
     	             **QuickSort(a, 0, 1)**
                          Input: [1.1]
                          a[] =  [1.1, 2.5, 3.5, 4.2, 9.2, 8.9, 6.4, 7.5]
                          Done. (**QuickSort(a, 0, 1)**)
     		     **QuickSort(a, 2, 3)**
                          Input: [3.5]
                          a[] =  [1.1, 2.5, 3.5, 4.2, 9.2, 8.9, 6.4, 7.5]
                          Done. (**QuickSort(a, 2, 3)**)
                   [1.1]
                   [3.5]
                   Concatented pieces = [1.1, 2.5, 3.5]
                   a[] = [1.1, 2.5, 3.5, 4.2, 9.2, 8.9, 6.4, 7.5]
     	      Done. (**QuickSort(a, 0, 3)**)
     
     	      **QuickSort(a, 4, 8)**
                   Input: [9.2, 8.9, 6.4, 7.5]
                   a[] = [1.1, 2.5, 3.5, 4.2, 9.2, 8.9, 6.4, 7.5]
                   Pivot = 7.5
                   After partition: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                          Input: [6.4]
                          a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                          Done.
                          Input: [8.9, 9.2]
                          a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                          Pivot = 9.2
                          After partition: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                                 Input: [8.9]
                                 a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                                 Done.
                                 Input: []
                                 a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                                 Done.
                          [8.9]
                          []
                          Concatented pieces = [8.9, 9.2]
                          a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
                   [6.4]
                   [8.9, 9.2]
                   Concatented pieces = [6.4, 7.5, 8.9, 9.2]
                   a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
            [1.1, 2.5, 3.5]
            [6.4, 7.5, 8.9, 9.2]
            Concatented pieces = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
            a[] = [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
     
     After sort:   [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
     ```

7. 现在我们首先来看看快速排序只的 **原地分割**的算法

   - 接下来，我将会用图示的方式一步一步讲解原地分割算法

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03.gif)

   - 算法描述

     - 首先在数组中，维护三个区间，如下图所示

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03a.gif)

     - **segment1**中是所有 小于等于 **pivot**的元素

     - **segment2**是所有 大于 **piovt**的元素

     - **segment3**中是不需要处理的元素

     - **segmet2 与 segment3**之间是一个空的插槽

     - 算法工作流如下所示

       - 如果 **a[ larger_I -1 ] > pivot **，则添加 **a[larger_I - 1]**到segment2

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03b.gif)
       -  如果**a [ larger_I - 1] <= pivot**，则添加 **a[larger_I - 1] ** 到segment1

         ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03c.gif)       

8. 原地分割算法的执行

   ``` Int  partition ( double [] a  , int iLeft , int iRight) {
         1、保存**piovt**到辅助变量中
   
              piovt = a[iRight - 1];
   
   Notice : 我们在数组中留了一个插槽    
   ```

   ![ ](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition04.gif)

         ```
   2、设置两个索引去分割**segment**
   
              Smaller_I = Left;
   
               Larger_I = bright - 1;
   
   Notice : 我们在数组中留了一个插槽
         ```

   ​      ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition05.gif)    

   

       ```
   3、 while( larger_I > smaller_I ) 
   
     {
       ```

   ​      ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03a.gif)

       ```
      If( a[ larger_i - 1 ] > pivot )
   
      {
   
       /*===============================================
     
      把a[larger_I - 1] 放入segment 2 并且减小  larget_I的值 
   
      ================================================*/
   
         a [ larger_I ] = a [ larger_I - 1];
   
         larget_I--;
       ```

   

   ​       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03b.gif)

     

   ```
      }
      else
      {
   /* ==================================================
   	     把 a[larger_I -1] 放入 Segment 1 并且移动 hole 到后一个
   	 ================================================== */
                      help = a[larger_I -1];
                      a[larger_I -1] = a[smaller_I];
                      a[smaller_I] = help;
                      smaller_I++；
   ```

      ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/quickSort/partition03c.gif)

   ```
      }
   }
   4. 把pivot放到合适的地方 
   
   	     a[larger_I] = pivot;
   
   5. 返回 pivot 在数组中的索引值
   
            return (larger_I);
       }
   ```

9. partition方法的Java实现

   ```
      public static int partition( double[] a, int iLeft, int iRight )
      {
         double   pivot;
         double   help;
         int      smaller_I, larger_I;
   
         smaller_I = iLeft;
         larger_I	= iRight-1;
         pivot = a[iRight-1];     // 初始化插槽位置为 a[iRight-1]
   
         while ( larger_I > smaller_I )
         {
          	 if ( a[larger_I -1] > pivot )
   	 {  /* ==================================================
      
            把a[larger_I - 1] 放入segment 2 并且减小  larget_I的值 
   
   	       ================================================== */        
               a[larger_I] = a[larger_I -1];
               larger_I--;
   	 }
            else
            {
               /* =================================================
                  a[larger_I -1] <= pivot, 索引:
            	  交换 a[smaller_I] 和 a[larger_I -1] 并且 把 smaller_I 向前移动 
                  ================================================= */
                help = a[larger_I -1];
                a[larger_I -1] = a[smaller_I];
                a[smaller_I] = help;
                smaller_I++;
            }
         }
   
         a[larger_I] = pivot;   // 把pivot 放入插槽 
   
         return larger_I;
      }
   ```

10. 现在在原地快速排序算法中使用原地分区算法的：

    ```
    /* ========================================================
            Sort:  a[iLeft] a[iLeft+1] .... a[iRight-1]
    	======================================================== */
    
         void  QuickSort( double[] a, int iLeft, int iRight )
         {
            if ( iRight - iLeft ≤ 1 )
    	{
    	   //当数组长度小于等于1时 ，直接return
    	   return;
            }
    
            k = partition( a, iLeft, iRight );
           // 在分割完数组后 返回 pivot 的位置 
    
        	QuickSort( a, iLeft, k );   // 对子子数组进行排序
    	    QucikSort( a, k+1, iRight); // 对右子数组进行排序
         }
    ```

    

