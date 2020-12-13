<h1>堆排序</h1>

1. 一般堆都用数组来表示

   - 堆是一种逻辑上是二叉树的结构，但是实际上排序的时候用的都是数组实现。

   - 记住，堆排序的数据都是存储在数组中，不是二叉链表中！！！

2. 大家思考一个问题，如何用数组来表示堆呢？

   - 如何用数组a[] 来表示堆呢？

     - 首先，在**a[1]**来存储根节点

       > Note:千万注意，不是数组 a[0]哟

     - 接着存储根节点的子节点，也就是第一层的节点，从左往右依次存入数组中

     - 接着存储第一层的子节点，也就是第二层的节点，从左往右依次存入数组中

     - ............

   - 来看个例子吧

     - 存储根节点到**a[1]**中

       ​      ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01d.gif)

     - 存储根节点的子节点，从左到右依次存储根节点的子节点（第一层节点）

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01e.gif)

       - 存储第二层节点，即依次从左到右存储第一层的所有子节点

         ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01f.gif)

         - 最后的结果如图所示

           ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01g.gif)

   3. 思考：为什么我们要把堆的节点存储在数组中？为什么是数组？

      - 在数组中的话，我们很容易获取某一个节点的父亲/孩子节点

      - 在数组中如何获取父亲/孩子节点？

        - **a[k]**的左孩子节点是**a[2*k]**
        - **a[k]**的右孩子节点是**a[2*k+1]**

      - Example

        - **a[1]**的孩子节点是**a[2]和a[3]**

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01h.gif)

        - **a[2]**节点的孩子节点是**a[4]和a[5]**

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01i.gif)

        - **a[3]**节点的孩子节点为**a[4]**

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01j.gif)

      - 那怎么找到**a[k]**的父亲节点呢

        - **a[k]**的父亲节点为**a[k/2]**

          > Note: <h4>a[1]</h4>没有父亲节点

        - Example
          -  **a[6]**的父节点为**a[3]**

            ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01k.gif)

          - **a[5]** 的父节点为**a[2]**

            ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01l.gif)

          - **a[4]**的父节点为**a[2]**

            ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/Heap01m.gif)

   4. 在Java中用数组定义堆结构

      - 用变量去表示Heap

        ```
         public class Heap
           {
              public double a[];     // 数组中的每个元素都代表堆中的一个节点
        			    
        
              public int NNodes;     // 这是定义堆中节点的个数,即数组长度
        
              ... 其他方法 ...
           }
        ```

      - 构造函数，初始化变量

        ```
        public class Heap
           {
              public double a[];     // 数组中的每个元素都代表堆中的一个节点
        
              public int NNodes;     // 这是定义堆中节点的个数
        
        /*================================================================
                  构造函数: 通过size来构造一个可以包含size个节点的堆
         ============================================================== */
              public Heap( int size )
              {
                 a = new double[ size + 1 ];   // a[0]不使用
        	       NNodes = 0;                  // 这个定义现在堆中已经有0个节点
              }
                  ... 其他方法 ...
           }
        ```

   5. 在学习堆排序之前，我们先回顾下二叉树相关概念

      - 二叉树

        - 定义：每个节点至多有两个节点的树

        - Example

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/bin-tree01.gif)

      - 左孩子与右孩子

        - 因为每一个节点至多有两个孩子节点，所以，我们用左孩子和右孩子来区分他们

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/headSort/bin-tree02.gif)

        - Note

          - 有许多节点只有左孩子节点
          - 有许多节点只有右孩子节点

      - 完全二叉树
        - 定义
          - 完全二叉树 = 二叉树的每一层都包含最大的节点数，即每一个节点都是二个子节点