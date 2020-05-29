# 面试中的JavaScript之数据结构和算法

## 数据结构

数据结构(data structure)是相互之间存在一种或多种特定关系的数据元素的集合，即带“结构”的数据元素的集合。常见的数据结构：数组、栈、队列、链表、树、图、字典树、散列表（哈希表）。

### 栈

栈的特点是：先进后出，或者说是后进先出，从栈顶放入元素的操作叫入栈，取出元素叫出栈。

```javascript
class Stack {
  constructor() {
    this.items = [];
  }
  push(element) { // 入栈
    this.items.push(element);
  }
  pop() { // 出栈
    return this.items.pop();
  }
  get peek() { // 末位
    return this.items[this.items.length - 1];
  }
  get isEmpty() { // 是否为空栈
    return !this.items.length;
  }
  get size() { // 长度
    return this.items.length;
  }
  clear() { // 清空栈
    this.items = [];
  }
}
const stack = new Stack();
console.log(stack.isEmpty); // true
stack.push(5); stack.push(8);
console.log(stack.peek); // 8
console.log(stack.size); // 2
stack.clear();
console.log(stack.isEmpty); // true
```

### 队列

队列与栈一样，也是一种线性表，不同的是，队列可以在一端添加元素，在另一端取出元素，也就是：先进先出。从一端放入元素的操作称为入队，取出元素为出队。

```javascript
class Queue {
  constructor(items){
    this.items = items || [];
  }
  enqueue(element) { // 入队
    this.items.push(element);
  }
  dequeue() { // 出队
    return this.items.shift();
  }
  front() { // 队头
    return this.items[0];
  }
  clear() { // 清除队列
    this.items = [];
  }
  get size() { // 队列长度
    return this.items.length;
  }
  get isEmpty() { // 判断队列是否为空
    return !this.items.length;
  }
  print() { // 打印
    console.log(this.items.toString());
  }
}
const queue = new Queue();
console.log(queue.isEmpty); // true
queue.enqueue("John");
queue.enqueue("Jack");
console.log(queue.size); // 2
console.log(queue.isEmpty); // false
queue.print(); // John,Jack
```

### 链表

链表是物理存储单元上非连续的、非顺序的存储结构，数据元素的逻辑顺序是通过链表的指针地址实现，每个元素包含两个结点，一个是存储元素的数据域 (内存空间)，另一个是指向下一个结点地址的指针域。根据指针的指向，链表能形成不同的结构，例如单链表，双向链表，循环链表等。

```javascript
class Node {
  constructor(element) {
    this.element = element;
    this.next = null;
  }
}
class LinkedList { // 链表
  constructor() {
    this.head = null;
    this.length = 0;
  }
  
  append(element) { // 追加元素
    const node = new Node(element);
    let current = null;
    if (this.head === null) {
      this.head = node;
    } else {
      current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = node;
    }
    this.length++;
  }
  
  insert(position, element) { // 任意位置插入元素
    if (position >= 0 && position <= this.length) {
      const node = new Node(element);
      let current = this.head;
      let previous = null;
      let index = 0;
      if (position === 0) {
        this.head = node;
        node.next = current;
      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;
      }
      this.length++;
      return true;
    }
    return false;
  }
  
  removeAt(position) { // 移除指定位置元素
    if (position > -1 && position < this.length) { // 检查越界值
      let current = this.head;
      let previous = null;
      let index = 0;
      if (position === 0) {
        this.head = current.next;
      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        previous.next = current.next;
      }
      this.length--;
      return current.element;
    }
    return null;
  }
  
  findIndex(element) { // 寻找元素下标
    let current = this.head;
    let index = -1;
    while (current) {
      if (element === current.element) {
        return index + 1;
      }
      index++;
      current = current.next;
    }
    return -1;
  }
  
  remove(element) { // 删除指定文档
    const index = this.findIndex(element);
    return this.removeAt(index);
  }

  isEmpty() {
    return !this.length;
  }

  size() {
    return this.length;
  }

  toString() { // 转为字符串
    let current = this.head;
    let string = "";
    while (current) {
      string += ` ${current.element}`;
      current = current.next;
    }
    return string;
  }
}
const linkedList = new LinkedList();
console.log(linkedList);
linkedList.append(2);
linkedList.append(6);
linkedList.append(24);
linkedList.append(152);
linkedList.insert(3, 18);
console.log(linkedList); // {length:5, head:{element: 2, next: {element: 6, next: {element: 24, next: {element: 18, next: {element: 152, next: null}}}}}}
console.log(linkedList.findIndex(24)); 
linkedList.removeAt(0); // 2
linkedList.findIndex(24) // 1
```

### 字典

字典：类似对象，以key，value存贮值。

```javascript
class Dictionary { 
  constructor() { 
    this.items = {};
  }
  
  set(key, value) {
    this.items[key] = value;
  }

  get(key) {
    return this.items[key];
  }

  remove(key) {
    delete this.items[key];
  }

  get keys() {
    return Object.keys(this.items);
  }

  get values() {
  /*
    也可以使用ES7中的values方法
    return Object.values(this.items)
  */
    return Object.keys(this.items).reduce((r, c, i) => {
      r.push(this.items[c]);
      return r;
    }, []);
  }
}
const dictionary = new Dictionary();
dictionary.set("Gandalf", "gandalf@email.com");
dictionary.set("John", "johnsnow@email.com");
dictionary.set("Tyrion", "tyrion@email.com");

console.log(dictionary);
console.log(dictionary.keys); // ["Gandalf", "John", "Tyrion"]
console.log(dictionary.values); // ["gandalf@email.com", "johnsnow@email.com", "tyrion@email.com"]
dictionary.remove("Gandalf");
console.log(dictionary.items); // {John: "johnsnow@email.com", Tyrion: "tyrion@email.com"}
```

### 二叉树

树是一种数据结构，它是由n（n>=1）个有限节点组成一个具有层次关系的集合。把它叫做 “树” 是因为它看起来像一棵倒挂的树，也就是说它是根朝上，而叶朝下的。它具有以下的特点：

- 每个节点有零个或多个子节点；
- 没有父节点的节点称为根节点；
- 每一个非根节点有且只有一个父节点；
- 除了根节点外，每个子节点可以分为多个不相交的子树；

```javascript
class NodeTree { 
  constructor(key) { 
    this.key = key; 
    this.left = null; 
    this.right = null; 
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(key) {
    const newNode = new NodeTree(key);
    const insertNode = (node, newNode) => {
      if (newNode.key < node.key) {
        if (node.left === null) {
          node.left = newNode;
        } else {
          insertNode(node.left, newNode);
        }
      } else {
        if (node.right === null) {
          node.right = newNode;
        } else {
          insertNode(node.right, newNode);
        }
      }
    };
    if (!this.root) {
      this.root = newNode;
    } else {
      insertNode(this.root, newNode);
    }
  }

  // 访问树节点的三种方式:中序,先序,后序
  inOrderTraverse(callback) {
    const inOrderTraverseNode = (node, callback) => {
      if (node !== null) {
        inOrderTraverseNode(node.left, callback);
        callback(node.key);
        inOrderTraverseNode(node.right, callback);
      }
    };
    inOrderTraverseNode(this.root, callback);
  }

  min(node) {
    const minNode = node => {
      return node ? (node.left ? minNode(node.left) : node) : null;
    };
    return minNode(node || this.root);
  }

  max(node) {
    const maxNode = node => {
      return node ? (node.right ? maxNode(node.right) : node) : null;
    };
    return maxNode(node || this.root);
  }
}
const tree = new BinarySearchTree();
tree.insert(11);
tree.insert(7);
tree.insert(5);
tree.insert(3);
tree.insert(9);
tree.insert(8);
tree.insert(10);
tree.insert(13);
tree.insert(12);
tree.insert(14);
tree.inOrderTraverse(value => {
  console.log(value); // 3,5,7,8,9,10,11,12,13,14
});
console.log(tree.min()); // {key: 3, left: null, right: null}
console.log(tree.max()); // {key: 14, left: null, right: null}
```

## 算法

数据结构和算法解决是 “如何让计算机更快时间、更省空间的解决问题”，因此需从执行时间和占用空间两个维度来评估数据结构和算法的性能，分别用时间复杂度和空间复杂度两个概念来描述性能问题，二者统称为复杂度，复杂度描述的是算法执行时间（或占用空间）与数据规模的增长关系。

算法的执行时间与每行代码的执行次数成正比，用 T(n) = O(f(n)) 表示，其中 T(n) 表示算法执行总时间，f(n) 表示每行代码执行总次数，而 n 往往表示数据的规模。这就是大 O 时间复杂度表示法。

```javascript
function aFun() {
  console.log("Hello, World!"); // 需要执行 1 次
  return 0; // 需要执行 1 次
} // 2 次运算，时间复杂度 O(1)，常数阶

function bFun(n) {
  for(let i = 0; i < n; i++) { // 需要执行 (n + 1) 次
    console.log("Hello, World!"); // 需要执行 n 次
  }
  return 0; // 需要执行 1 次
} //  2n +2 次运算，时间复杂度 O(n)，线性阶
```

常用的时间复杂度所耗费的时间从小到大依次是：`O(1) < O(logn) < (n) < O(nlogn) < O(n2) < O(n3) < O(2n) < O(n!) < O(nn)`

### 排序算法

1.冒泡排序：

```javascript
const bubbleSort = arr => {
  const len = arr.length
  if(len <= 1) return arr
  for(let i=0; i<len-1; i++){
    for(let j=0; j<len-i-1; j++){
      if(arr[j] > arr[j+1]){
        const temp = arr[j]
        arr[j] = arr[j+1]
        arr[j+1] = temp
      }
    }
  }
  return arr
}
bubbleSort([1,2,8,3,6,0]) // [0, 1, 2, 3, 6, 8]

const bubbleSort2 = arr => {
  const length = arr.length;
  if (length <= 1) return arr;
  for (let i = 0; i < length - 1; i++) {
    let hasChange = false; // 提前退出冒泡循环的标志位
    for (let j = 0; j < length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        hasChange = true; // 表示有数据交换
      }
    }
    if (!hasChange) break; // 如果 false 说明所有元素已经到位，没有数据交换，提前退出
  }
  return arr;
};
bubbleSort2([7, 8, 4, 5, 6, 3, 2, 1]) // [1, 2, 3, 4, 5, 6, 7, 8]
```

2.插入排序：插入排序又为分为 直接插入排序 和优化后的 拆半插入排序 与 希尔排序

```javascript
const insertionSort = array => {
  const len = array.length;
  if (len <= 1) return array;
  let preIndex, current;
  for (let i = 1; i < len; i++) {
    preIndex = i - 1; //待比较元素的下标
    current = array[i]; //当前元素
    while (preIndex >= 0 && array[preIndex] > current) {
      //前置条件之一: 待比较元素比当前元素大
      array[preIndex + 1] = array[preIndex]; // 将待比较元素后移一位
      preIndex--; //游标前移一位
    }
    if (preIndex + 1 != i) {
      //避免同一个元素赋值给自身
      array[preIndex + 1] = current; //将当前元素插入预留空位
      console.log('array :', array);
    }
  }
  return array;
};
insertionSort([5, 4, 3, 2, 1]);
// [4, 5, 3, 2, 1]
// [3, 4, 5, 2, 1]
// [2, 3, 4, 5, 1]
// [1, 2, 3, 4, 5]

// 折半插入排序
const binaryInsertionSort = array => {
  const len = array.length;
  if (len <= 1) return array;
  let current, i, j, low, high, m;
  for (i = 1; i < len; i++) {
    low = 0;
    high = i - 1;
    current = array[i];
    while (low <= high) {
      //步骤 1 & 2 : 折半查找
      m = (low + high) >> 1; // 注: x>>1 是位运算中的右移运算, 表示右移一位, 等同于 x 除以 2 再取整, 即 x>>1 == Math.floor(x/2) .
      if (array[i] >= array[m]) {
        //值相同时, 切换到高半区，保证稳定性
        low = m + 1; //插入点在高半区
      } else {
        high = m - 1; //插入点在低半区
      }
    }
    for (j = i; j > low; j--) {
      //步骤 3: 插入位置之后的元素全部后移一位
      array[j] = array[j - 1];
      console.log('array2-1:', JSON.parse(JSON.stringify(array)));
    }
    array[low] = current; //步骤 4: 插入该元素
  }
  console.log('array2-2:', JSON.parse(JSON.stringify(array)));
  return array;
};
binaryInsertionSort([5, 4, 3, 2, 1])
// array2-1: (5) [5, 5, 3, 2, 1]
// array2-1: (5) [4, 5, 5, 2, 1]
// array2-1: (5) [4, 4, 5, 2, 1]
// array2-1: (5) [3, 4, 5, 5, 1]
// array2-1: (5) [3, 4, 4, 5, 1]
// array2-1: (5) [3, 3, 4, 5, 1]
// array2-1: (5) [2, 3, 4, 5, 5]
// array2-1: (5) [2, 3, 4, 4, 5]
// array2-1: (5) [2, 3, 3, 4, 5]
// array2-1: (5) [2, 2, 3, 4, 5]
// array2-2: (5) [1, 2, 3, 4, 5]
```

3.选择排序：选择排序空间复杂度为 O(1)，是一种原地排序算法；是一种不稳定的排序算法；时间复杂度`T(n) = O(n2)`

```javascript
const selectionSort = array => {
  const len = array.length;
  let minIndex, temp;
  for (let i = 0; i < len - 1; i++) {
    minIndex = i;
    for (let j = i + 1; j < len; j++) {
      if (array[j] < array[minIndex]) {
        // 寻找最小的数
        minIndex = j; // 将最小数的索引保存
      }
    }
    temp = array[i];
    array[i] = array[minIndex];
    array[minIndex] = temp;
    console.log('array: ', array);
  }
  return array;
};
selectionSort([5, 4, 3, 2, 1]) // [1, 2, 3, 4, 5]
// array:  (5) [1, 4, 3, 2, 5]
// array:  (5) [1, 2, 3, 4, 5]
// array:  (5) [1, 2, 3, 4, 5]
// array:  (5) [1, 2, 3, 4, 5]
```

4.快速排序:

```javascript
function quickSort(arr) {
  if (arr.length<=1) {return arr;}
    var left = [],
    right = [],
    baseDot =Math.round(arr.length/2),
    base =arr.splice(baseDot, 1)[0];

  for (var i =0; i <arr.length; i++) {
    if (arr[i] < base) {
      left.push(arr[i])
    }else {
      right.push(arr[i])
    }
  }
  return quickSort(left).concat([base], quickSort(right));
}

function quickSort(array, left, right) {
  var length =array.length,
    left =typeof left ==='number'? left :0,
    right =typeof right ==='number'? right : length-1;

  if (left < right) {
    var index = left -1;
    for (var i = left; i <= right; i++) {
      if (array[i] <= array[right]) {
        index++;
        var temp = array[index];
        array[index] = array[i];
        array[i] = temp;
      }
    }
    quickSort(array, left, index -1);
    quickSort(array, index +1, right);
  }
  return array;
}
```

### 斐波那契

第三项等于前面两项之和：

```javascript
function fibonacci(n){
  if(n === 0) return 0;
  if(n === 1 || n === 2 ) return 1;
  return fibonacci(n-1) + fibonacci(n-2);
}

function fibonacci(n, current = 0, next = 1) {
  if(n === 1) return next;
  if(n === 0) return 0;
  return fibonacci(n - 1, next, current + next);
}

function fibonacci(n) {
  let current = 0, next = 1, temp;
  for(let i = 0; i < n; i++){
    temp = current;
    current = next;
    next += temp;
  }
  return current;
}

function fibonacci(n){
  let seed = 1;
  return [...Array(n)].reduce(p => {
    const temp = p + seed; 
    seed = p;
    return temp;
  }, 0)
}

function* fibonacci(){
  let current = 0, next = 1;
  yield current;
  yield next;
  while(true) {
    [current, next] = [next, current + next];
    yield next;
  }
}
```

### 动态规划

通过全局规划，将大问题分割成小问题来取最优解。比如最少硬币找零，美国有以下面额(硬币）：d1=1, d2=5, d3=10, d4=25，如果要找36美分的零钱，我们可以用1个25美分、1个10美分和1个便士（ 1美分)。

```javascript
class MinCoinChange {
  constructor(coins) {
    this.coins = coins
    this.cache = {}
  }

  makeChange(amount) {
    if (!amount) return []
    if (this.cache[amount]) return this.cache[amount]
    let min = [], newMin, newAmount
    this.coins.forEach(coin => {
      newAmount = amount - coin
      if (newAmount >= 0) {
        newMin = this.makeChange(newAmount)
      }
      if (newAmount >= 0 && 
      (newMin.length < min.length - 1 || !min.length) && 
      (newMin.length || !newAmount)) {
        min = [coin].concat(newMin)
      }
    })
    return (this.cache[amount] = min)
  }
}
const rninCoinChange = new MinCoinChange([1, 5, 10, 25])
console.log(rninCoinChange.makeChange(36)) // [1, 10, 25]
const minCoinChange2 = new MinCoinChange([1, 3, 4])
console.log(minCoinChange2.makeChange(6)) // [3, 3]
```

### 贪心算法

贪心算法（又称贪婪算法）是指，在对问题求解时，总是做出在当前看来是最好的选择。同样是解决硬币问题

```javascript
function MinCoinChange1(coins) {
  var coins = coins;
  var cache = {};
  this.makeChange = function(amount) {
    var change = [], total = 0;
    for (var i = coins.length; i >= 0; i--) {
      var coin = coins[i];
      while (total + coin <= amount) {
        change.push(coin);
        total += coin;
      }
    }
    return change;
  };
}
const minCoinChange = new MinCoinChange([1, 5, 10, 25]);
console.log(minCoinChange.makeChange(36)); // [25, 10, 1]
console.log(minCoinChange.makeChange(34)); // [25, 5, 1, 1, 1, 1]
console.log(minCoinChange.makeChange(6)); // [5, 1]
```

### 二分查找

给定一个排序好的数组，用二分查找的办法找出目标元素

```javascript
const binarySearch = function(ary, target) {
  if (!Array.isArray(ary)) {
    throw new TypeError("arg1 is not a array");
  }
  let start = 0,
  end = ary.length - 1;
  while (start <= end) {
    let mid = Math.floor(start + (end - start) / 2);
    if (ary[mid] === target) {
      return mid;
    } else if (ary[mid] < target) {
      start = mid + 1;
    } else {
      end = mid - 1;
    }
  }
  return -1;
};
```

### 其他

数组洗牌（数组乱序）：将数组中的数字，打乱顺序，保证每个位置的概率相等

```javascript
const flush = function(num = []) {
  for (let i = 0; i < num.length; i++) {
    let index = Math.floor(Math.random() * (num.length - 1));
    let temp = num[i];
    num[i] = num[index];
    num[index] = temp;
  }
  return num
};

function shuffle(arr){
  let m = arr.length;
  while(m > 1){
    let index = parseInt(Math.random() * m--);
    [arr[index],arr[m]] = [arr[m],arr[index]];
  }
  return arr;
}
```

集合的子集：输入集合`[A,B]`，输出`[],[A],[B],[A,B]`

```javascript
var subsets = function(nums) {
  let result = [];
  function dfs(index,ans){
    let ans2 = ans.concat();
    ans2.push(nums[index]);
    if(index === 0){
      result.push(ans);
      result.push(ans2);
      return;
    }else{
      dfs(index-1,ans);
      dfs(index-1,ans2);
    }
  }
  dfs(nums.length-1,[]);
  return result;
};
```

参考文章：

- [一个前端眼中的斐波那契数列](https://juejin.im/entry/5ab452b56fb9a028d3755376)
- [JavaScript 排序，不只是冒泡](https://juejin.im/entry/59250db844d904006cefa11f)
- [JavaScript 数据结构与算法之美 - 冒泡排序、插入排序、选择排序](https://juejin.im/post/5d341a89f265da1bac405369)
- [MDN JavaScript教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [JS 原生面经从初级到高级【近1.5W字】](https://juejin.im/post/5daeefc8e51d4524f007fb15?utm_source=gold_browser_extension#heading-130)
- [JS快速排序&三路快排](https://juejin.im/post/5c662e496fb9a049b82afb71)
- [“寒冬”三年经验前端面试总结（含头条、百度、饿了么、滴滴等）之手写题（一）](https://juejin.im/post/5d9eef20e51d45781332e961#heading-0)