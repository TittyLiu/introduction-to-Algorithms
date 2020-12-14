<h2>The Binary Search Tree

1. 二叉树：把节点放入二叉树中

   - 定义：二叉搜索树 =  一颗满足如下条件的二叉树

     - 节点x的所有左子树的值小于x的值
     - 节点x的所有右子树的值大于x的值

   - Example

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04.gif)

     > Notes：注意二叉树中每一个节点的属性

     - Node 3 ：

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04a.gif)

     - Note 1:

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04b.gif)

     - Note 6:

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04c.gif)

     - Note 9:

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04d.gif)

2. 为什么称为二叉搜索树呢？

   - 因为在二叉搜索树中查找一个特定的值非常容易。

   - Example：在二叉搜索树中搜索节点的值为7

     ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04.gif)

   - 怎么做才能找到节点的值为7的节点呢

     - 首先从根节点出发

     ​           ![img](http://www.mathcs.emory.edu/~cheung/Courses/171/Syllabus/9-BinTree/FIGS/BST06.gif)

     ​          因为**7 > 3**, 搜索二叉搜索树的右节点

     - 继续，从右子树的根节点开始

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST06a.gif)

       ​       因为** 7 > 6,**所以在其右子树中搜索

     - 继续

       ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST06b.gif)

       ​                   因为 ** 7 < 9,**所以在其左子树中搜素

     - 最后，7终于找到！！！

   3. 如果搜索一个不存在的值会发生什么?

      - 事实上，如果我们搜索一个不存在的值，他会在空节点的父亲节点处停止

      - Example：在下面的二叉树中搜索值为10的节点。

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04.gif)

      -  现在来看看怎样搜索值为10的节点

        - 还是从根点开始搜索

        ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST07.gif)

        ​            因为**7 > 3,**，所以在右子树中国搜索。

        - 继续

           ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST07a.gif) 因为 **7 > 6,**所以在其右子树中搜索

        - 继续搜索

          ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST07b.gif)

          因为 **10 > 9,**所以在其右子树中搜索</br>

        - 停止搜索!!!!!!

          - 节点9的右子树节点一个空的子树

          - 注意，在二叉搜索树中节点9是节点10的父节点

            ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST07c.gif)

            我们可以试着在节点9的右子树中添加节点10。

      4. 二叉树搜索树具有许多有用的性质，我们现在来看看

         - 递归属性

           - 如果**T**是一个以x为根节点二叉搜索树，则：

             - x的左子树也是一颗二叉搜索树
             - x的右子树也是一颗二叉搜索树

           - Example：

             ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST04a.gif)

         - 如何在二叉搜索树中找到最小值呢？

           - 可以通过如下方式获得二叉搜索树中的最小值
             - 从根节点开始
             - 从根节点的左节点开始遍历左节点直到某一个节点的左节点为空
               - 这个节点的值就是我们要找到最小值

           - Example

             - 二叉搜索树中的最小值如下所示：

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST13a.gif)

             - 在如下的二叉搜索树中查找最小值

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST13b.gif)

             - 请注意，由于子树也是二叉搜索树，因此我们可以使用相同的技术在子树中找到最小值。下面是右子树中最小值

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST13c.gif)

         - 如何在二叉搜索树中查找最大值

           - 通过下面的方式可以在二叉搜索树找到最大值
             - 首先从根节点开始查找
             - 从右节点开始，遍历每一个节点的右子树，直到某一个节点的右子树为空
               - 此时，这个值就是我们找的最大值

           - Example

             - 在下列的最大值中查找最大值

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST14a.gif)

             - 在如下的二叉搜索树中查找最大值

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST14b.gif)

             - 请注意，由于子树以及二叉搜索树，我们可以使用相同的技术在子树中找到最大值！在左子树中查找最大值

               ![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/BST/BST14c.gif)

