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

       