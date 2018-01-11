### 一些算法的实现(JS篇)

#### 1. 冒泡排序
##### 代码:
```
// 分类 -------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- O(n^2)
// 最优时间复杂度 ---- 如果能在内部循环第一次运行时,使用一个旗标来表示有无需要交换的可能,可以把最优时间复杂度降低到O(n)
// 平均时间复杂度 ---- O(n^2)
// 所需辅助空间 ------ O(1)
// 稳定性 ------------ 稳定

var arr1 = [7,12,4,23,21,2,17,13,6,33]

//升序
function bubbleSortUp (arr) {
  var len = arr.length
  for(var i = 0; i < len - 1; i++) {
    for(var j = i +1; j < len; j++) {
      if(arr[j] < arr[i]) {  //比较后面的和前面的大小
        var tmp = arr[i]  //后面大的话就和当前的交换
        arr[i] = arr[j]
        arr[j] = tmp    //当前一定是未排序的最小值
      }
    }
  }
  return arr
}

//降序
function bubbleSortLow (arr) {
  var len = arr.length
  for(var i = 0; i < len - 1; i++) {
    for(var j = i +1; j < len; j++) {
      if(arr[j] > arr[i]) { //比较后面的和前面的大小
        var tmp = arr[i]    //后面小的话就和当前的交换
        arr[i] = arr[j]
        arr[j] = tmp     //当前一定是未排序的最大值
      }
    }
  }
  return arr
}

var arrUp = bubbleSortUp(arr1)
console.log(arrUp)

var arrLow = bubbleSortLow(arr1)
console.log(arrLow)
```

#### 2. 快速排序
##### 代码:
```
// 分类 ------------ 内部比较排序
// 数据结构 --------- 数组
// 最差时间复杂度 ---- 每次选取的基准都是最大（或最小）的元素，导致每次只划分出了一个分区，需要进行n-1次划分才能结束递归，时间复杂度为O(n^2)
// 最优时间复杂度 ---- 每次选取的基准都是中位数，这样每次都均匀的划分出两个分区，只需要logn次划分就能结束递归，时间复杂度为O(nlogn)
// 平均时间复杂度 ---- O(nlogn)
// 所需辅助空间 ------ 主要是递归造成的栈空间的使用(用来保存left和right等局部变量)，取决于递归树的深度，一般为O(logn)，最差为O(n)       
// 稳定性 ---------- 不稳定

var arr1 = [7,12,4,23,21,2,17,13,6,33]

//升序
function quickSortUp (arr) {
  var len = arr.length
  if(len <= 1) return arr

  //可随意指定一个存在的数为基准数，一般为首尾或者中
  var base_index = 0
  var base_num = arr[0]  
  var arr_left = [], arr_right = []  
  for(var i = 1; i < len - 1; i++) {
    if(base_num > arr[i] ) { //小于基准数的都放到左边的数组里
      arr_left.push(arr[i])  
    } else {                 //大于基准数的都放到右边的数组里
      arr_right.push(arr[i])
    }
  }
  arr_left = quickSortUp(arr_left)   //递归左边再排序
  arr_right = quickSortUp(arr_right) //递归右边再排序
  return arr_left.concat([base_num] , arr_right)
}

//降序
function quickSortLow (arr) {
  var len = arr.length
  if(len <= 1) return arr

  //可随意指定一个存在的数为基准数，一般为首尾或者中
  var base_index = 0
  var base_num = arr[0]  
  var arr_left = [], arr_right = []  
  for(var i = 1; i < len - 1; i++) {
    if(base_num > arr[i] ) { //小于基准数的都放到右边的数组里
      arr_right.push(arr[i])  
    } else {                 //大于基准数的都放到左边的数组里
      arr_left.push(arr[i])
    }
  }
  arr_left = quickSortUp(arr_left)   //递归左边再排序
  arr_right = quickSortUp(arr_right) //递归右边再排序
  return arr_left.concat([base_num] , arr_right)
}

var arrUp = quickSortUp(arr1)
console.log(arrUp)

var arrLow = quickSortLow(arr1)
console.log(arrLow)


```

#### 3. 选择排序
##### 代码:
```
// 分类 -------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- O(n^2)
// 最优时间复杂度 ---- O(n^2)
// 平均时间复杂度 ---- O(n^2)
// 所需辅助空间 ------ O(1)
// 稳定性 ------------ 不稳定

var arr1 = [7,12,4,23,21,2,17,13,6,33]

//升序
function selectSortUp (arr) {
  var len = arr.length
  for(var i = 0; i < len - 1; i++) {  //i为已排序的末尾项
    var min = i  
    for(var j = i +1; j < len; j++) {  //未排序的序列
      if(arr[j] < arr[min]) {  //找到未排序序列的最小项
        min = j  
      }
      if(min != i) {  //交换未排序最小项和已排序的末尾项
        var tmp = arr[i]
        arr[i] = arr[min]
        arr[min] = tmp
      }
    }
  }
  return arr
}

//降序
function selectSortLow (arr) {
  var len = arr.length
  for(var i = 0; i < len - 1; i++) {  //i为已排序的末尾项
    max = i
    for(var j = i +1; j < len; j++) { //未排序的序列
      if(arr[j] > arr[max]) {  //找到未排序序列的最大项
        max = j
      }
      if(max != i) {  //交换未排序最大项和已排序的末尾项
        var tmp = arr[i]
        arr[i] = arr[j]
        arr[j] = tmp  
      }
    }
  }
  return arr
}

var arrUp = selectSortUp(arr1)
console.log(arrUp)

var arrLow = selectSortLow(arr1)
console.log(arrLow)

```

#### 4. 堆排序
##### 代码:
```
// 分类 -------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- O(nlogn)
// 最优时间复杂度 ---- O(nlogn)
// 平均时间复杂度 ---- O(nlogn)
// 所需辅助空间 ------ O(1)
// 稳定性 ------------ 不稳定

var arr1 = [7,12,4,23,21,2,17,13,6,33]

function maxHeapify (array, i, heapSize) {
    var iMax, iLeft, iRight
    while(true) {
        iMax = i
        iLeft = 2 * i + 1
        iRight = 2 * i + 2
        if (iLeft < heapSize && array[iMax] < array(iLeft)>) {
            iMax = iLeft
        }
        if (iRight < heapSize && array[iMax] < array(iRight)>) {
            iMax = iRight
        }
        if(iMax == i) break

        let tmp = array[i]
        array[i] = array[iMax]
        array[iMax] = tmp
        i = iMax        
    }
}

function buildMaxHeap(array) {
    var i, iParent = Math.floor(array.length / 2) - 1;

    for (i = iParent; i >= 0; i--) {
      maxHeapify(array, i, array.length);
    }
}

function heapSortLow(array) {
    buildMaxHeap(array);

    for (var i = array.length - 1; i > 0; i--) {
      swap(array, 0, i);
      maxHeapify(array, 0, i);
    }
    return array;
}

var arrLow = heapSortLow(arr1)
console.log(arrLow)

```

#### 5. 插入排序
插入排序最稳定
##### 代码:
```
// 分类 ------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- 最坏情况为输入序列是降序排列的,此时时间复杂度O(n^2)
// 最优时间复杂度 ---- 最好情况为输入序列是升序排列的,此时时间复杂度O(n)
// 平均时间复杂度 ---- O(n^2)
// 所需辅助空间 ------ O(1)
// 稳定性 ------------ 稳定

var arr1 = [7,12,4,23,21,2,17,13,6,33]

//升序
function insertSortUp (arr) {
  var len = arr.length
  if(len <= 1) return arr
  for(var i = 1; i < len - 1; i++) {  //i为未排序的首项
    if(arr[i] < arr[i-1]) { //当前项小于前一项
        var tmp = arr[i] //保存当前项的值
        var j = i - 1
        //大于当前已排序的项后移 
        while(j >= 0 && arr[j] > tmp) { 
            arr[j+1] = arr[j]
            j--
        }
        //插入到已排序项的中间位置(大于前者，小于后者)
        $arr[j+1] = tmp
    }
  }
  return arr
}

//降序
function insertSortLow (arr) {
  var len = arr.length
  if(len <= 1) return arr
  for(var i = 1; i < len - 1; i++) {  //i为已排序的末尾项
    if(arr[i] > arr[i-1]) { //当前项小于前一项
      var tmp = arr[i] //保存当前项的值
      var j = i - 1
      //小于当前已排序的项后移 
      while(j >= 0 && arr[j] < tmp) {
        arr[j+1] = arr[j]
        j--
      }
      //插入到已排序项的中间位置(小于前者，大于后者)
      $arr[j+1] = tmp
    }
  }
  return arr
}

var arrUp = selectSortUp(arr1)
console.log(arrUp)

var arrLow = selectSortLow(arr1)
console.log(arrLow)

```
时间复杂度O(n^2)

#### 6. 希尔排序
##### 代码:
```
// 分类 -------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- 根据步长序列的不同而不同。已知最好的为O(n(logn)^2)
// 最优时间复杂度 ---- O(n)
// 平均时间复杂度 ---- 根据步长序列的不同而不同。
// 所需辅助空间 ------ O(1)
// 稳定性 ------------ 不稳定


```

#### 7. 归并排序
##### 代码:
```
// 分类 -------------- 内部比较排序
// 数据结构 ---------- 数组
// 最差时间复杂度 ---- O(nlogn)
// 最优时间复杂度 ---- O(nlogn)
// 平均时间复杂度 ---- O(nlogn)
// 所需辅助空间 ------ O(n)
// 稳定性 ------------ 稳定



```


#### 8. 基数排序
##### 代码:
```



```

#### 9.二分查找
##### 代码:
```


```