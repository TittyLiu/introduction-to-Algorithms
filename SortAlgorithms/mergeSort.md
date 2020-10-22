

# 归并排序

1. 合并两个数组

   **问题：**假设现在我们有两个数组，如下所示：</br>

   - `Example:`

   - **`  a = [2.5, 3.5, 6.4, 7.5]      `  **

   - **` b = [1.1, 8.9, 9.2] `**

   - 需要我们设计一个算法去合并着两个数组为一个数组，并且为合并后的数组必须是有序的，你会怎么办呢？

   

**解决方法：**

- 假设**i**和**j**分别指向**a**数组和**b**数组的第一个元素
  
- 对比**a[i]** 和**b[j]**
  
  ```
         i=0                        j=0
          |                          |
          V                          V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [ ] 
     
  ```
  
- 对比后找到两者中最小的数，把这个数作为结果拷贝到Result数组里面，然后移动较小值的数组中的索引，较大值的数组索引保持不变(即*i*不变，*j*向后移动一位)
  
  ```
         i=0                             j=1
          |                               |
          V                               V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1]
  ```
  
- 接着比较 **a[i]** 和 **b[j]**  （2.5  > 8.9?）       
  
  ```
         i=0                             j=1
          |                               |
          V                               V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1]
  ```
  
- 把较小值拷贝到Result中去，然后移动较小值数组的索引值(现在**i**向后移动一位)
  
  ```
              i=1                        j=1
               |                          |
               V                          V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1, 2.5]
  ```
  
- 继续比较**a[i]**和**b[j]**（3.5 > 8.9?）
  
  ```
              i=1                        j=1
               |                          |
               V                          V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1, 2.5] 
  ```
  
- .................经过**n**轮的对比和拷贝操作，直到数组的**a**到达了尾部，此时对比**a[i]**和**b[j]**
  
  ```
                        i=2              j=1
                         |                |
                         V                V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1, 2.5, 3.5, 6.4]
  ```
  
- 因为7.5 小于 8.9，所以把7.5 拷贝到Result数组中，然后移动**i**的索引值
  
  ```
                          i=3 !!         j=1
                            |             |
                            V             V
        [2.5, 3.5, 6.4, 7.5]       [1.1, 8.9, 9.2]    
     
     
        Result: [1.1, 2.5, 3.5, 6.4, 7.5]
  ```
  
- > Note：现在需要注意，数组a已经结束了
  

  
- 如果一个数组已经遍历结束了，记住就不要在继续执行**比较操作**啦，应该把遍历还没结束的数组中的所有值，直接添加到Result中
  
2. 算法实现

   - **Given：**

     ​        1):  两个分别已经有序的数组**a**和**b**</br>

     ​        2): 一个大小**a.size() + b.size()**的result数组</br>

   - **Task:**

   ​               合并两个已经有序的数组**a**和**b**到一个排完序的**result**数组中

   - **C++ Code：**

     ```
      void merge(vector<double> result, vector<double> a, vector<double> b)      
        {
           int i, j, k;
     
           i = j = k = 0;
     
           while ( i < a.size() || j < b.size() )
           {
            	 if ( i < a.size() && j < b.size() ){  
            	 // 此时两个数组中都有元素
                 if ( a[i] < b[j] )
     	               result[k++] = a[i++];
                 else
                      result[k++] = b[j++];
     	 }else if ( i == a.size() )
                 result[k++] = b[j++];     // a 为空时
     	 else if ( j == b.size() )
                 result[k++] = a[i++];     // b 为空时
           }
        }
     ```
   
3. 现在来开始看下简单的合并排序算法是如何一步一步进行而来

```
  Sort an array a[ ] of number:
       1. 把数组a[]的前部分(即a[0,middle-1])分割为一个left[] 的数组
       2. 把数组a[]的后半部分(即a[middle,a.size()-1])分割为一个right[]的数组
       3. 对分割完的数组left[]和right[]数组分别进行排序
       4. 最后把两个排好序的数组再进行一次排序，结果放到一个result数组中
```

- 例子

  ```
  Sort:       [6.4, 3.5, 7.5, 2.5, 8.9, 4.2, 9.2, 1.1]
               /                    \
  		       /       分割成两部分      \
  		     /                          \
      [6.4, 3.5, 7.5, 2.5]        [8.9, 4.2, 9.2, 1.1]
                       |                         |
   对两个数组分别进行排序  | (E.g.: 可以使用冒泡排序)  ｜ 
  		                 V                         V
             [2.5, 3.5, 6.4, 7.5]        [1.1, 4.2, 8.9, 9.2]
                       \                        /
  		                  \  最后合并两个有序数组   /
  		                   \                    /
  	         	[1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
  ```

  - C++ Code

    ```
       void sort(vector<double> a)
       {
          vector<double> left, right;
    
          if ( a.size() == 1 )
          {
             // 数组长度为1，不需要排序 !
             return;
          }
      /*============================================================
      Split      a[0 ..... middle-1   middle .... a.length-1]
                            /                  \
          left[0 .. middle-1]       right[0 ... a.length-1-middle]
           =========================================================== */
          int middle = a.size()/2;    //新建一个数组保存数组a的前面部分 
    
          for ( int i = 0; i < middle; i++ )
             left.push_back(a[i]) ;
    
          for ( int i = 0; i < a.length-middle; i++ )
             right.push_back(a[i+middle]);
             
          /* ======================================
              我们这里使用冒泡排序对left[]和right[]数组分别进行排序
             ====================================== */
          BubbleSort.sort( left );   //调用冒泡排序对left[]排序
          BubbleSort.sort( right );  //对right调用冒泡排序
    
          /* ====================================== 
             对排完序的数组进行合并排序，并拷贝到a数组中
           ====================================== */
          merge( a, left, right );   // 之前我们已经讨论过merge算法啦
       }
    ```

    - 代码输出

      ```
    Sort:    [6.4, 3.5, 7.5, 2.5, 8.9, 4.2, 9.2, 1.1]
      Split:   [6.4, 3.5, 7.5, 2.5] | [8.9, 4.2, 9.2, 1.1]   

      Sorted Left half:  [2.5, 3.5, 6.4, 7.5]
      Sorted Right half: [1.1, 4.2, 8.9, 9.2]
      
      Result: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
      ```

    - 冒泡排序

      ```
    public class BubbleSort1
      {
     public static void sort(vector<double> a)
         {
            double help;  // 辅助变量，辅助交换数组
            int i, k;
            boolean done;
       /* ---------------------------------------------------
                   选择排序算法
      --------------------------------------------------- */
            done = false;
            k = a.length;
      
            while ( ! done )
            {
               done = true;           // shSet tripwire
      
               /* ===========================================
                    对无序数组a[k..n]进行排序(n = a.length)
               =========================================== */
               for ( i = 0 ; i < k-1 ; i ++ )
               {
                  if ( a[i] > a[i+1] )
                  {
        /* ---------------------------------------------------
                  交换a[i]和a[i+1]
         --------------------------------------------------- */
                     help = a[i];
                     a[i] = a[i+1];
                     a[i+1] = help;
      
                     done = false;    // tripwire activated !!!
                  }
               }
      
               k--;
            }
         }
      }
      ```
      

    > 其实，我们未必一定要使用冒泡排序去排序两个数组，我们也可以考虑使用归并排序

  

  4.这一章我们讨论的归并排序算法，并没有考虑算法效率问题，所以，我们称它为原始版本归并排序算法，在这个版本的算法中，我们在每一次递归过程中会创建许多临时数组，在下一章我们将会介绍基本的归并算法

  - 考虑下面的简化版的归并排序算法

  ```
   void sort(vector<double> a)
     {
        vector<double> left, right;
  
        if ( a.size() == 1 )
        {
           // 如果待排数组只有一个元素，则不需要排序!
           return;
        }
      /*========================================================
   分割数组      a[0 ..... middle-1  middle .... a.length-1]
                      /                     \
    left[0 .. middle-1]       right[0 ... a.length-1-middle]     ======================================================= */
        int middle = a.length/2;
  
        for ( int i = 0; i < middle; i++ )
           left.push_back(a[i]);
  
        for ( int i = 0; i < a.size()-middle; i++ )
           right.push_back(a[i+middle]);
  
        /* ======================================
               使用冒泡排序对两个无序数组进行排序
           ====================================== */
        BubbleSort.sort( left );       
        BubbleSort.sort( right );      
  
        /* ======================================
               对两个数组进行合并并排序，然后拷贝给愿数组
        ====================================== */
        merge( a, left, right );   // 调用我们在第一部分将过的merge算法
     }
  ```

  > **Idea：**其实合并排序算法的功能和冒泡排序算法的功能相似，让我们现在开始使用归并排序算法吧！

  - 归并排序算法

    ```
     void sort(vector<double> a)
       {
          vector<double> left, right;
    
          if ( a.size() == 1 )
          {
             return;
          }
        /*========================================================
     分割数组    a[0 ..... middle-1  middle .... a.length-1]
                      /                  \
      left[0 .. middle-1]       right[0 ... a.length-1-middle]        ======================================================= */
          int middle = a.length/2;
    
          for ( int i = 0; i < middle; i++ )
             left.push_back(a[i]);
    
          for ( int i = 0; i < a.size()-middle; i++ )
             right.push_back(a[i+middle] ;
    
          /* ======================================
             现在，我们使用MergeSort算法来对两个数组进行排序！！！
             ====================================== */
           sort( left );       // 递归调用    
           sort( right );      // 递归调用    
           
          /* ======================================
                  把合并完毕后的有序结果返回
             ====================================== */
          merge( a, left, right );   // 调用之前讲过的merge算法
       }
    ```

    - 测试样例

      ```
      Before sort: [6.4, 3.5, 7.5, 2.5, 8.9, 4.2, 9.2, 1.1]
      
      After  sort: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]      
      ```

    - 算法工作流程

      - ```
        算法将会一直递归的对输入的数组进行分割，直到数组里面只有一个元素
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up001.gif)

        ```
        当递归到数组只有一个元素，停止递归，返回 10.2
        ```

      - ```
        第二次排序对递归最底层右边数据6.4进行排序
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up002.gif)

         ```
        发现它同时也只有一个数6.4，所以sort函数返回6.4
         ```

      - ```
        现在把数组[10.2,6.4]分割后的两部分都已经有序，将会调用merge函数，进行合并操作
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up003.gif)

      -  ```
        调用merge函数返回归并后的结果
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up004.gif)

      -    ```
        现在开始对 [3.5,7.5] 进行排序
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up005.gif) 

        ```
        数组[3.5,7.5]开始分割，因为分割后侧数组只有一个元素，sort函数返回3.5和7.5
        ```

      - ```
        因为两个数组就只有一个数且排完序，故开始调用merge函数进行归并操作
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up006.gif)

      - ```
        将[3.5,7.5]归并完的结果将会被返回
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up007.gif)

      - ```
        现在[10.2,6.4]以及[3.5,7.5]两个待排数组已经有序，对两个有序数组调用merge函数，进行归并操作
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up008.gif)

      - ```
        归并后的结果返回
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up009.gif)

      - ```
        然后右边也执行相同的操作.....
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up010.gif)

      - ```
        最后对返回两个数组调用merge
        ```

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up011.gif)

    - ```
      算法实现流程
      ```

      ```
      Input: [6.4, 3.5, 7.5, 2.5, 8.9, 4.2, 9.2, 1.1]
      
             Sort: [6.4, 3.5, 7.5, 2.5, 8.9, 4.2, 9.2, 1.1]
             Split:[6.4, 3.5, 7.5, 2.5] | [8.9, 4.2, 9.2, 1.1]        
                    Sort: [6.4, 3.5, 7.5, 2.5]
                    Split:[6.4, 3.5] | [7.5, 2.5]
                           Sort: [6.4, 3.5]
                           Split:[6.4] | [3.5]
                                  Sort: [6.4]
                                  Result: [6.4]
                           Sorted Left half:  [6.4]
                                  Sort: [3.5]
                                  Result: [3.5]
                           Sorted Right half: [3.5]
                           Merged Result: [3.5, 6.4]
                    Sorted Left half:  [3.5, 6.4]
                           Sort: [7.5, 2.5]
                           Split:[7.5] | [2.5]
                                  Sort: [7.5]
                                  Result: [7.5]
                           Sorted Left half:  [7.5]
                                  Sort: [2.5]
                                  Result: [2.5]
                           Sorted Right half: [2.5]
                           Merged Result: [2.5, 7.5]
                    Sorted Right half: [2.5, 7.5]
                    Merged Result: [2.5, 3.5, 6.4, 7.5]
             Sorted Left half:  [2.5, 3.5, 6.4, 7.5]
                    Sort: [8.9, 4.2, 9.2, 1.1]
                    Split:[8.9, 4.2] | [9.2, 1.1]
                           Sort: [8.9, 4.2]
                           Split:[8.9] | [4.2]
                                  Sort: [8.9]
                                  Result: [8.9]
                           Sorted Left half:  [8.9]
                                  Sort: [4.2]
                                  Result: [4.2]
                           Sorted Right half: [4.2]
                           Merged Result: [4.2, 8.9]
                    Sorted Left half:  [4.2, 8.9]
                           Sort: [9.2, 1.1]
                           Split:[9.2] | [1.1]
                                  Sort: [9.2]
                                  Result: [9.2]
                           Sorted Left half:  [9.2]
                                  Sort: [1.1]
                                  Result: [1.1]
                           Sorted Right half: [1.1]
                           Merged Result: [1.1, 9.2]
                    Sorted Right half: [1.1, 9.2]
                    Merged Result: [1.1, 4.2, 8.9, 9.2]
             Sorted Right half: [1.1, 4.2, 8.9, 9.2]
             Merged Result: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
      
      Output: [1.1, 2.5, 3.5, 4.2, 6.4, 7.5, 8.9, 9.2]
      ```


  5.改进的自顶向下的归并排序

  - > 问题：上面的原始版本的归并算法在每次执行时都会创建许多数组，因此，我们需要重写上面的归并算法

    

  - ```
    一个效率更高的方法是通过给sort函数传递两个想要排序的范围作为行参，如下所示：
    sort( vector<double> a, int left, int right )    
         {
            ...
         }
       //每个行参意义
         a   = 我们想要排序的输入数组
         
        sort()方法排序的范围:     
             a[left]  a[left+1] ....  a[right-1]
    ```

  - 现在我们来看下具体算法

    ```
    /* ==================================================
                 sort()方法将会对下面元素进行排序:
    
                  a[left] a[left+1] ... a[right-1]
           ================================================== */
      
      sort( vector<double> a,  int left, int right )
        {
          vector<double> left, right;
    
          if ( (right-left) == 1 )
          {
             // 数组中只有一个元素，不需要排序！!
             return;
          }
    
       ************************** NEW ***************************
    
          /*============================================================
       分割数组    a[left ..... middle-1  middle .... right-1]
                            /                  \
             a[left .. middle-1]       right[middle ... right-1]      =========================================================== */     
          int middle = (right + left)/2;
          sort( a, left, middle );       // Sort left array
          sort( a, middle, right );      // Sort right array 
    
    /* ==========================================================
                把所有的排序好的数组进行归并返回    ========================================================== */
          merge( a, left, middle, right );   // 归并 !!!
       }
    ```

  - > 现在需要注意，我们以前merge()方法接受三个数组作为参数，因为我们已经修改了sort()方法，sort函数不需要在每次创建临时数组，只需传递数组排序的范围即可，所以相对应地merge()方法也需要修改，只需要传递一个数组作为行参即可

    ```
    merge函数形式:
    
             merge( double[] a, int left, int middle, int right )               
    
    注意:现在merge只需传递一个数组a[]，还必须有两个值用于分割数组:
    
             left part:   a[left] a[left+1] ... a[middle-1]
             right part:  a[middle] a[middle+1] ... a[right-1]     
    
     排完序以后的数组:
    
             a[left] a[left+1] .....  a[right-1] 
    ```

  - 图解 merge(vector<double> a, int left , int right)

    ```
    假设我们调用merge函数 merge( a, 0, 2, 4) 它将会合并两个子数组:
      left part:  a[0] a[1]       (因为 middle = 2, so 2-1 = 1)
      right part: a[2] a[3]       (因为 right  = 4, so 4-1 = 3)     
    ```

  **Example:**

  ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up032.gif)

  ​     

  调用merge(a , 0 , 2, 4) 将会完成下面过程：</br>   

  ​         ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up033.gif)

- 现在把修改后的归并算法用于merge sort算法

  - 看下原始merge算法和修改后的merge算法区别

    - ```
      原始merge算法使用2个数组
         left[ ]:   left[0] left[1] ...
         right[ ]:  right[0] right[1] ....     
       
       修改后的merge算法使用2个相同的数组
          left part:   a[left] a[left+1] ... a[middle-1]
          right part:  a[middle] a[middle+1] ... a[right-1]   
      
      我们需要创建一个临时数组投保存归并结果（否则将会覆盖原始数组）  
      
      ```

  - 可视化算法过程

    创建一个临时数组tmp[]</br>

    ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up035.gif)

    把第一次归并的数据添加到临时数组中</br>

    ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up036.gif)

  ​    继续把归并后的结果保存到tmp里面   </br>![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up037.gif)

   继续对剩下的数进行归并，并保存到tmp数组中</br>

​    ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up038.gif)

  .........................</br>

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up039.gif)

当我们执行一次归并结束，需要把归并结果(保存在tmp数组中的结果)拷贝到数组a[]中

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/merge_top_up040.gif)

- C++ implement  Code

  ```
  /* ======================================================           
        Merge函数执行过程中做了如下工作:
  
        1. 为了归并两个数组，创建了临时数组tmp[]
  
        2. 把归并两个邻接数组的结果保存到tmp[]数组中
  
              left array (已排序)         right array (已排序)
             a[iLeft ... iMiddle-1]      a[iMiddle... iRight]
                     \                         /
                      \                       /  排序
                       \                     /
                      tmp[ iLeft ... iRight ]
                                  |
                                  | 拷贝到原始数组 !
                                  V
                        a[ iLeft... iRight ]
  `
        3. 每执行已merge操作都需要把这次的结果(tmp数组中的值)拷贝到原始数组a[]中
        The SAME portion of the array tmp[ ] is used !!!
        
        ====================================================== */
     void Merge(vector<double> a,
                              int iLeft, int iMiddle, int iRight)
     {
        int i, j, k;
  
        vector<double> tmp; //创建临时数组
  
        i = iLeft;     // 持续调整数组索引
        j = iMiddle;
        k = iLeft;
  
        while ( i < iMiddle || j < iRight )    // 下面的内容几乎和以前的merge函数相同!    
        {
           if ( i < iMiddle && j < iRight )
           {  // 两个数组都不为空时
              if ( a[i] < a[j] )
                 tmp.push_back(a[i++]) ;
              else
                 tmp.push_back(a[j++]) ;
           }
           else if ( i == iMiddle )
              tmp.push_back(a[j++]) ;      // a数组 为空时
           else if ( j == iRight )
              tmp.push_back(a[i++]);      // b数组 为空时
        }
  
        /* =================================
           拷贝归并结果到原始数组a[] 中
           ================================= */
        for ( i = iLeft; i < iRight; i++ )
           a[i] = tmp[i];
     }
     
  ===============================================================   
     
     //原始merge算法
     
       void merge(vector<double> result, vector<double> a, vector<double> b)      
     {
        int i, j, k;
  
        i = j = k = 0;
  
        while ( i < a.size() || j < b.size() )
        {
         	 if ( i < a.size() && j < b.size() )
  	 {  // a数组和b数组都不为空时
              if ( a[i] < b[j] )
  	       result[k++] = a[i++];
              else
                 result[k++] = b[j++];
  	 }
           else if ( i == a.size(()) )
              result[k++] = b[j++];     // a 数组为空
  	 else if ( j == b.size() )
              result.push_back(a[i++]) ;     // b 数组为空
        }
     }
  ```

  > Notes:通过对比原始和修改后的merge算法，发现他们之间的区别很小，所以这也给我们一个启示：
  >
  > - - **Good programmers** do **not re-invent** the **tool (e.g., screwdriver**) to solve a ***slightly\* modified problem**, they ***adjust\*** the **tool \**!!!\****

- ​        但是同时要注意，修改后的merge() 方法也有一个缺点，在每次创建过程都会产生许多垃圾，因为在每次执行一次merge函数都修改把tmp数组中的内容拷贝到数组a[]中，在C++中，我们可以使用**&**引用，这样就不必拷贝数组，在Java中，只需在所有的sort结束后在执行拷贝即可，即在sort()方法中定义一个全局变量，传递给merge()函数

  ```
  C++ Code
  void merge(vector<int>  &nums,int lo ,int mid,int ){
     //C++ 通过引用不需要拷贝数组啦，直接传递引用即可
      int n1 = mid - lo + 1;
      int n2 = hi - mid;
      
      int L[n1],R[n2];
      for(int i = 0;i < n1;i++)
         L[i] = nums[lo+i];
      for(int j = 0;j<n2;j++)
         R[j]=nums[mid + 1 + j];
      
      int i = 0,j=0,k=lo;       //这里定义k和给k赋值的时候需要注意
      while(i <n1 && j < n2){   //这里的while其实改成for循环也可以
          if(L[i] < R[j])
              nums[k++]=L[i++];
          else
              nums[k++] = R[j++];
      }
      while(i < n1)
          nums[k++] = L[i++];
      while(j < n2)
          nums[k++] = R[j++];
  }
  
  
  ==============Java Code=================
  
  public static void Merge(double[] a,
                              int left, int leftEnd, int rightEnd,      
                              double[] tmp)
     {
        // 现在我们不需要创建一个临时数组了 !!!!
  
        int i, j, k, left_orig;
  
        i = left; j = leftEnd;
        k = left;
  
        while ( i < leftEnd || j < rightEnd )
        {
  	 if ( i < leftEnd && j < rightEnd )
  	 {  // Both array have elements
              if ( a[i] < a[j] )
  	       tmp[k++] = a[i++];
              else
  	       tmp[k++] = a[j++];
  	 }
  	 else if ( i == leftEnd )
              tmp[k++] = a[j++];	   // left 边数组为空
  	 else if ( j == rightEnd )
              tmp[k++] = a[i++];	   // right 边数组为空
        }
  
        //拷贝结果回原始数组
        for ( i = left; i < rightEnd; i++ )
  	       a[i] = tmp[i];
     } 
  
  ```

  

```
完整的自顶向上算法（Java Code）
public static void sort(double[] a, int left, int right, double[] tmp)
    {
      double[] left, right;

      if ( (right-left) == 1 )
      {
         // 数组元素长度为1，不需要拷贝 !
         return;
      }
******************** Same as the sort() above *********************
********************   except things in red   *********************      /* =================================================================
     分割数组     a[left ..... middle-1  middle .... right-1]
                            /                  \
              a[left .. middle-1]       right[middle ... right-1]
 ================================================================= */     
      int middle = (right + left)/2;
      
      sort( a, left, middle, tmp ); // 循环递归调用
      sort( a, middle, righ, tmp ); // 循环递归调用

    /* ==========================================================
                 把归并结果拷贝到数组a中
     ========================================================== */
       merge( a, left, middle, right, tmp );   //通过tmp来帮助排序 !!!
   }

```

6.自底向上的归并排序</br>

`自底向上的归并排序算法思想`</br>

1. 首先，我们把数组中相邻的每个元素作为一对，分别进行对比排序</br>

2. 把数组中相邻的2个元素作为一对，分别进行对比排序</br>

3. 把数组中的相邻的4个元素作为一对，分别进行排序</br>

4. ...........</br>


**Simple example**</br>

- 输入数组：

   **`   6.4   3.5   7.5   2.5   8.9   4.2   9.2   1.1        `**

- 第一次遍历：

  ​    **Merge** **pairs** of **adjacent arrays** of **size = 1**:

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/Bottom-upMerge001.gif)



- 第二次遍历：

   **Merge** **pairs** of **adjacent arrays** of **size = 2**:

  ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/buttom-upMerge002.gif)

- 第三次遍历：

​        **Merge** **pairs** of **adjacent arrays** of **size = 4**:

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/buttom-upMerge003.gif)

- 直到整个数组有排，排序结束！

**仔细观察排序过程**

- 在每一次遍历过程中，数组中的每个元素都涉及许多次**merge** 操作
  - 让我们在回顾一下上面三幅图片,我们发现每个元素都有箭头指向它，这意味着该元素涉及到排序操作了
- 根据观察结果，在后面我们会根据观察结果，来稍微改进merge



**简化版的自底而上的merge Sort**

1. 简化版假设

   - 假设数组元素为2的n次幂$2^n$

2. 假设数组元素如下所示，遍历过程如下所示

   - Iteration 1

     - **`Array elements merged with each other:       `**

     - ` 0    1   2   3   4   5   6   7   8   9   10   11   12   13`     

     - ` (L) (R) (L) (R) (L) (R) (L) (R) (L) (R)  (L)  (R)  (L)  (R)`      

     - 

     - `a[0] with a[1] `

     - `a[2] with a[3] `

     - `......`

     - `每个合并的数组中只有一个元素`

     ​     **可视化**

     ​         ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/Bottom-upMerge004.gif)

   - Iteration 2
     - **`   Array elements merged with each other:      `   **

     - 

     - **`0   1   2   3   4   5   6   7   8   9   10   11   12   13`                `  -------   -----  ------  ------  ------   -------  -------- `

     - `     (L)        (R)     (L)     (R)     (L)      (R)       (L) `    

     -  a[0] a[1] with a[2] a[3]    </br>

     -  a[4] a[5] with a[6] a[7]    </br>

     -  .......        </br>

     -   每个需要合并的数组中有2个元素</br>

     - **可视化**

     - ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/Bottom-upMerge005.gif)

     -  

   - Iteration 3

      **`Array elements merged with each other:      `**

     **`0   1   2   3   4   5   6   7   8   9   10   11   12  13..               -------------     -------------   ---------------   --------              (L)                  (R)                 (L)           (R)           `**

     `a[0] a[1] a[2]  a[3]  with a[4]  a[5]  a[6]  a[7]   `

     `a[8] a[9] a[10] a[11] with a[12] a[13] a[14] a[15]     `

     `... `...     

     `每一次合并的数组有四个元素**

<h3>总结</h3>

- 在第一次遍历过程中，合并数组长度width=1的操作如下：

- ````
      merge( a, left = 0, middle = 1, right = 2 )            
      merge( a, left = 2, middle = 3, right = 4 )
      merge( a, left = 4, middle = 5, right = 6 )
      ...
   Or:
  
      merge( a, left = 0*width, middle = 1*width, right = 2*width )    
      merge( a, left = 2*width, middle = 3*width, right = 4*width )
      merge( a, left = 4*width, middle = 5*width, right = 6*width )
      ...
  ````

- 在第二次遍历过程中，合并数组长度width=2 *(new width)= 2*old width)，合并过程如下：

  ```
      merge( a, left = 0, middle = 2, right = 4 )            
      merge( a, left = 4, middle = 6, right = 8 )
      merge( a, left = 8, middle = 10, right = 12 )
      ...
  
   Or:
  
      merge( a, left = 0*width, middle = 1*width, right = 2*width )    
      merge( a, left = 2*width, middle = 3*width, right = 4*width )
      merge( a, left = 4*width, middle = 5*width, right = 6*width )
      ...
  
  ```

- 在第三次遍历过程中，**width = 4**,(new width = 2 * old width),合并过程如下所示：

  ```
      merge( a, left = 0, middle = 4, right = 8 )            
      merge( a, left = 8, middle = 12, right = 16 )
      ...
  
   Or:
  
      merge( a, left = 0*width, middle = 1*width, right = 2*width )    
      merge( a, left = 2*width, middle = 3*width, right = 4*width )
      merge( a, left = 4*width, middle = 5*width, right = 6*width )
      ...
  ```

- 上面的简化版的自底向上的代码如下所示：

  ```
     void sort(vector<double> a)
     {
        int width;
  
        for ( width = 1; width < a.size(); width = 2*width )      
        {
           // Combine pairs of array a of width "width"
           int i;
           for ( i = 0; i < a.size(); i = i + 2*width )
           {
              int left, middle, right;
              left = i;
              middle = i + width;
              right  = i + 2*width;
              merge( a, left, middle, right );
           }
        }
     }
  ```

> Note

```
外层循环如下所示：
for ( width = 1; width < a.length; width = 2*width )    
   {
       // 每次循环的过程中，width将会取得 2的k次幂(=$2^k$)
       //    iter 1: width = 1 ($2^0$)
       //    iter 2: width = 2 ($2^1$)
       //    iter 3: width = 4 ($2^2$)
       //  .......
   }

```

​        因此，merge(a,left,middle,right):

```
for ( i = 0; i < a.size(); i = i + 2*width )     
    {
        // i ONLY takes on value that are powers of 2

        int left, middle, right;

        left = i;               // left is a power of 2
        middle = i + width;
        right  = i + 2*width;   // right is a power of 2     

        merge( a, left, middle, right );
    }
```

 <h3>组织算法结构</h3>

-  Merge() 方法需要一个临时数组去保存合并完的元素，但是定义一个局部数组变量，程序将会产生许多开销
- 但是如果换个思路，新建一个临时数组变量来保存需要合并的数组，然后，所有的合并操作在这个数组上进行，合并后只需返回临时数组就可以了

  **改进的算法**

  ```
  void sort(vector<double> a, vector<double> tmp )
   {
      int width;

      for ( width = 1; width < a.size(); width = 2*width )      
      {
         // Combine pairs of array a of width "width"
         int i;

         for ( i = 0; i < a.size(); i = i + 2*width )
         {
            int left, middle, right;

            left = i;
            middle = i + width;
            right  = i + 2*width;

            merge( a, left, middle, right, tmp );
         }
      }
   }

  ```



<h2>算法的实现步骤如下</h2>

```
/* ======================================================           
      Merge过程如下:

      1. 对两个邻接数组调用merge函数进行合并排序操作，把合并后的数据保存到tmp数组中 
            left array (sorted)         right array (sorted)
           a[iLeft ... iMiddle-1]      a[iMiddle... iRight]
                   \                         /
                    \                       /  排序然后合并
                     \                     /
                    tmp[ iLeft ... iRight ]
                                |
                                | 把结果返回给原始数组a !
                                V
                      a[ iLeft... iRight ]
`
      2. 把排完序和合并的结果(此结果保存在tmp数组里面)复制到原始数组a中

      The SAME portion of the array tmp[ ] is used !!!
      ====================================================== */
    void Merge(vector<double> a,
                            int iLeft, int iMiddle, int iRight,
                            vector<double> tmp)
   {
      int i, j, k;

      i = iLeft;     // 重新调整数组
      j = iMiddle;
      k = iLeft;

      while ( i < iMiddle || j < iRight )    // It's the same algorithm !    
      {
         if ( i < iMiddle && j < iRight )
         {  // 两个数组同时都存在元素
            if ( a[i] < a[j] )
               tmp[k++] = a[i++];
            else
               tmp[k++] = a[j++];
         }
         else if ( i == iMiddle )
            tmp[k++] = a[j++];      // a 数组为空时
         else if ( j == iRight )
            tmp[k++] = a[i++];      // b 数组为空时
      }

      /* =================================
         每执行完一遍合并，就把tmp[]中的结果拷贝到数组a[]
         ================================= */
      for ( i = iLeft; i < iRight; i++ )
         a[i] = tmp[i];
   }

```

<h3>优化算法</h3>

- 在每次合并后，其实不必把数组tmp中的结果拷贝给原始数组a

  ```
   void Merge(vector<double>[] a,
                              int iLeft, int iMiddle, int iRight,
                              vector<double> tmp)
     {
        int i, j, k;
  
        i = iLeft;     // 重新调整索引
        j = iMiddle;
        k = iLeft;
  
        while ( i < iMiddle || j < iRight )    // It's the same algorithm !    
        {
           if ( i < iMiddle && j < iRight )
           {  // Both array have elements
              if ( a[i] < a[j] )
                 tmp[k++] = a[i++];
              else
                 tmp[k++] = a[j++];
           }
           else if ( i == iMiddle )
              tmp[k++] = a[j++];      // a is empty
           else if ( j == iRight )
              tmp[k++] = a[i++];      // b is empty
        }
  
        /* ========================================
           每次合并后都会把tmp数组中的结果拷贝到数组a中(需要优化)
           ======================================== */
        for ( i = iLeft; i < iRight; i++ )
           a[i] = tmp[i];
     }
  
  ```

  **我们把拷贝操作在所有的merge结束后再进行，也就是把拷贝放到sort中去，如下所示：**

  ```
    void sort(vector<double> a, vector<double> tmp )
     {
        int width;
  
        for ( width = 1; width < a.size(); width = 2*width )      
        {
           // Combine pairs of array a of width "width"
           int i;
  
           for ( i = 0; i < a.size(); i = i + 2*width )
           {
              int left, middle, right;
  
              left = i;
              middle = i + width;
              right  = i + 2*width;
  
              merge( a, left, middle, right, tmp );  // Merge
           }
  
           /* ===============================================
              All merge() are done for ONE complete iteration
  
  	    NOW we copy tmp[ ] back to a[ ]
  	    =============================================== */
            for ( i = 0; i < a.length; i++ )
               a[i] = tmp[i];
        }
     }
  
  ```

  **修改后的完整代码如下所示**

  ```
   void sort(vector<double> a, vector<double> tmp)
     {
        int width;
  
        for ( width = 1; width < a.length; width = 2*width )
        {
         	 // 合并两个长度为**width**的数组
  	 int i;
  
  	 for ( i = 0; i < a.length; i = i + 2*width )
  	 {
              int left, middle, right;
  
              left = i;
              middle = i + width;
              right  = i + 2*width;
  
              merge( a, left, middle, right, tmp );
  
  	 }
  /* ========================================================
  	    现在不用每次都在merge函数后执行拷贝操作，这样子效率太低，把拷贝操作放到sort函数中，在所有的merge函数执行完毕后，开始拷贝
  ======================================================== */     
  	 for ( i = 0; i < a.length; i++ )
              a[i] = tmp[i];
        }
     }
     
  //改进后的merge函数   
   void merge(vector<double> a,
                              int iLeft, int iMiddle, int iRight,      
                              vector<double> tmp)
     {
        int i, j, k;
  
        i = iLeft;
        j = iMiddle;
        k = iLeft;
  
        while ( i < iMiddle || j < iRight )
        {
         	 if ( i < iMiddle && j < iRight )
  	 {  // Both array have elements
              if ( a[i] < a[j] )
  	       tmp[k++] = a[i++];
              else
                 tmp[k++] = a[j++];
  	 }
           else if ( i == iMiddle )
              tmp[k++] = a[j++];	   // a 为空时
  	 else if ( j == iRight )
              tmp[k++] = a[i++];	   // b 为空时
        }
  
        // 拷贝函数被我们移除了
     }
  
  ```

  

  

  