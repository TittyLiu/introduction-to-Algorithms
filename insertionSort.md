插入排序
=======
`思想:` 插入排序,是将数据分为已排序、未排序两部分</br>
	 1、从未排序的数中，取出一个元素</br>
	 2、把上面步骤中取出的元素，在已排序中从后往前依次对比，直到遇到一个小于自己的元素并插入在该元素后面，若没有找到比自己小的数，则插在最前面</br>
	 3、重复以上步骤，直到数据元素全部有序</br>

	<p> 看完了思想，画图在好好理解下：</p>

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort001.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort002.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort003.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort004.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort005.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort006.png)

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertionSort007.png)

-----------

上面只是插入排序的一部分，现在我们来看下动图，加深一下理解</br>

![](https://raw.githubusercontent.com/TittyLiu/staticResource/master/images/sortImages/insertion_sort.gif)
根据上面的思路，我们写下了如下插入排序的代码:</br>  

```
  void insertionSort(vector<int> &arr){
	for(int i = 1;i < arr.size();i++){
	    for(int j = i;j >= 0;j--){
	        if(arr[j] < arr[j -1]){
	            int temp = arr[j];
	            arr[j] = arr[j - 1];
	            arr[j-1] = temp;
	        }
	    }
	}
}
```
问题：这个代码有什么问题呢，咋看之下没什么问题，要实现的功能也都实现了，其实不然，这个代码的效率太低了，现在我们来分析一下这个时间复杂度，在最坏情况下，这个程序需要执行$frac{N^2}{2}$次比较和交换，最好情况下，$需要进行N-1次比较，0 次交换$ </br>
改进：我们把内层循环中的每次交换两个元素改为向右移动，这样子的话，我们访问数组的次数就减少一半</br>

```
void insertionSort(vector<int> &arr){
	 for(int i = 0;i < arr.size();i++){
	    int key = arr[i];
	    while(arr[i-1] > arr[i]){
	        arr[i] = arr[i-11];
	        i--;
	     }
	    arr[i]=key;
	 }
	}
```

​	

