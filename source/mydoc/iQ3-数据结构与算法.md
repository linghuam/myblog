## 数分解成很多个质数相乘

## 从一个无序，不相等的数组中，选取N个数，使其和为M实现算法？

## 你对算法数据结构了解多少？链表和数组区别？
- 数组：顺序存储，读取快速，插入和删除要移动大量元素，不方便。
- 链表：链式存储，读取要从头开始，麻烦，但插入和删除方便，只用修改指针即可。
- 数组静态分配内存，链表动态分配内存；
- 数组在内存中连续，链表不连续；
- 数组元素在栈区，链表元素在堆区；
- 数组利用下标定位，时间复杂度为O(1)，链表定位元素时间复杂度O(n)；
- 数组插入或删除元素的时间复杂度O(n)，链表的时间复杂度O(1)。

## 二分查找？
二分法查找，也称折半查找，是一种在有序数组中查找特定元素的搜索算法。查找过程可以分为以下步骤：
1. 首先，从有序数组的中间的元素开始搜索，如果该元素正好是目标元素（即要查找的元素），则搜索过程结束，否则进行下一步。
2. 如果目标元素大于或者小于中间元素，则在数组大于或小于中间元素的那一半区域查找，然后重复第一步的操作。
3. 如果某一步数组为空，则表示找不到目标元素。

```js
// 递归算法
function binary_search(arr,low, high, key) {
    if (low > high){
        return -1;
    }
    var mid = parseInt((high + low) / 2);
    if(arr[mid] == key){
        return mid;
    }else if (arr[mid] > key){
        high = mid - 1;
        return binary_search(arr, low, high, key);
    }else if (arr[mid] < key){
        low = mid + 1;
        return binary_search(arr, low, high, key);
    }
};
var arr = [1,2,3,4,5,6,7,8,9,10,11,23,44,86];
var result = binary_search(arr, 0, 13, 10);
alert(result); // 9 返回目标元素的索引值
```

## 排序算法知道多少种？适用场景是什么（有序性，数据规模，稳定性等）？冒泡什么时候复杂度最高？
十大经典排序算法总结：https://www.cnblogs.com/jztan/p/5878630.html
- 冒泡排序：o(n^2)，稳定
- 选择排序：每次从剩余的数中选择最小值，依次放到数组中，o(n^2)，不稳定
- 插入排序：先取出已排好的序列，从其他数中依次取出与已排序序列比较，插入到已排序序列中，o(n^2)，稳定
- 希尔排序：将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，不稳定
- 归并排序：将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序，稳定
- 快速排序：分治法，一次将数据分成两部分，一部分比关键字小，一部分比关键字大，不稳定
- 堆排序
- 计数排序
- 桶排序
- 基数排序

## 前端都会用到什么算法？说到了虚拟 DOM 的 diff 算法，又问虚拟 DOM 和真实 DOM 哪个快？
diff 采用逐层比较而不是遍历整棵树的方式提高效率。

虚拟 DOM 效率高于 真实 DOM，因为它只改变数据变化的部分，而操作真实DOM很可能引起页面重排与重绘。

虚拟DOM不会进行排版与重绘操作

虚拟DOM进行频繁修改，然后一次性比较并修改真实DOM中需要改的部分（注意！），最后并在真实DOM中进行排版与重绘，减少过多DOM节点排版与重绘损耗

真实DOM频繁排版与重绘的效率是相当低的

虚拟DOM有效降低大面积（真实DOM节点）的重绘与排版，因为最终与真实DOM比较差异，可以只渲染局部（同2）

## 树的广度和深度优先遍历?
- 广度：分层，队列
- 深度：对每一个可能的分支路径深入到不能再深入为止，而且每个节点只能访问一次，栈

### 冒泡排序？
n 个数进行 n-1 次比较，每次比较进行 n-i 次。

每次比较最大的数就放到最后，所以每次比较后只需对前几个进行。

正序时间复杂度为 o(n)，逆序时间复杂度为 o(n^2)，排序稳定。

```js
function bubbleSort(arr){
  var len = arr.length;
  var i,j,temp;
  for ( i = 0; i < len-1; i++){
    for (j = 0; j < len-i-1; j++){
      if (arr[j] > arr[j+1]){
        temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
  return arr;
}
```

