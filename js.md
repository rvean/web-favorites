<h1 align="center">JavaScript</h1>

<b><details><summary>1. JavaScript 中如何检测一个变量是 String 类型</summary></b>

三种方法 typeof、constructor、Object.prototype.toString.call()

```js
// typeof
typeof('123') === "string" // true
typeof '123' === "string" // true

// constructor
'123'.constructor === String // true

// Object.prototype.toString.call
Object.prototype.toString.call('123') === '[object String]' // true
```

</details>

<b><details><summary>2. 请用 js 去除字符串空格</summary></b>

+ replace 正则

```js
// 去除所有空格:
str = str.replace(/\s+/g, '')

// 去除两头空格:
str = str.replace(/^\s+|\s+$/g, '')

// 去除左空格:
str = str.replace(/^\s*/, '')

// 去除右空格:
str = str.replace(/(\s*$)/g, '')
```

+ .trim() 方法，用来删除字符串两端的空白字符并返回

</details>

<b><details><summary>3. == 和 === 的不同</summary></b>

== 是抽象相等运算符，而 === 是严格相等运算符。== 运算符是在进行必要的类型转换后，再比较。=== 运算符不会进行类型转换，所以如果两个值不是相同的类型，会直接返回false

```js
1 == "1"; // true
1 == [1]; // true
1 == true; // true
0 == ""; // true
0 == "0"; // true
0 == false; // true
```

</details>

<b><details><summary>4. 如何添加、移除、移动、复制、创建和查找节点</summary></b>

+ 创建新节点
```js
createDocumentFragment() // 创建一个 DOM 片段
createElement() // 创建一个具体的元素
createTextNode() // 创建一个文本节点
```

+ 添加、移除、替换、插入
```js
appendChild() // 添加
removeChild() // 移除
replaceChild() // 替换
insertBefore() // 插入
```

+ 查找
```js
getElementById() // 通过元素 Id
getElementsByTagName() // 通过标签名称
getElementsByName() // 通过元素的 Name 属性的值
```

</details>

<b><details><summary>5. 事件委托(事件代理)是什么</summary></b>

事件委托：利用事件冒泡的原理，让自己的所触发的事件，让他的父元素代替执行

+ 适合用事件委托的事件：click，mousedown，mouseup，keydown，keyup，keypress
+ 不适合的就有很多了，举个例子，mousemove 每次都要计算它的位置，非常不好把控。还有 focus、blur 之类的，本身就没用冒泡的特性，自然就不用事件委托了

优点：
1. 大量减少内存占用，减少事件注册
2. 新增元素实现动态绑定事件

> 提高性能，而且新添加的元素还会有之前的事件
```js
<ul>
  <li>苹果</li>
  <li>香蕉</li>
  <li>凤梨</li>
</ul>
// 利用事件委托 绑定父元素
document.querySelector('ul').onclick = event => {
  let target = event.target
  if (target.nodeName === 'LI') {
    console.log(target.innerHTML)
  }
}
```

+ 事件冒泡与事件委托的对比
  - 事件冒泡：box 内部无论是什么元素，点击后都会触发 box 的点击事件
  - 事件委托：可以对 box 内部的元素进行筛选

+ 事件委托获取索引
```js
<ul id="ul">
  <li>1111</li>
  <li>点击获取下标</li>
  <li>3333</li>
</ul>

<script>
  window.onload = function () {
    let oUl = document.getElementById("ul");
    let aLi = oUl.getElementsByTagName("li");
    oUl.onclick = function (ev) {
      let ev = ev || window.event;
      let target = ev.target || ev.srcElement;
      if (target.nodeName.toLowerCase() == "li") {
        let that = target;
        let index;
        for (let i = 0; i < aLi.length; i++)
          if (aLi[i] === target) index = i;
        if (index >= 0) alert('我的下标是第' + index + '个');
        target.style.background = "red";
      }
    }
  }
</script>
```

</details>

<b><details><summary>6. require 与 import 的区别</summary></b>

1. 加载方式不同，require 是在运行时加载，而 import 是在编译时加载
2. 规范不同，require 是 CommonJS/AMD 规范，import 是 ESMAScript6+规范
3. require 特点：社区方案，提供了服务器/浏览器的模块加载方案。非语言层面的标准。只能在运行时确定模块的依赖关系及输入/输出的变量，无法进行静态优化。
import 特点：语言规格层面支持模块功能。支持编译时静态分析，便于 JS 引入宏和类型检验。动态绑定。

</details>

<b><details><summary>7. 对象的几种创建方式</summary></b>

1. Object 构造函数创建
```js
var Person = new Object()
Person.name = "Nike"
Person.age = 27
```

2. 使用对象字面量表示法
```js
var Person = {
	name: 'Nike',
	age: 27
}
```

3. 使用工厂模式创建对象
```js
function createPerson(name, age, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function() {
    alert(this.name);
  };
  return o;
}
var person1 = createPerson("Nike", 29, "teacher");
var person2 = createPerson("Arvin", 20, "student");
```

4. 使用构造函数创建对象
```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() {
    alert(this.name);
  };
}
var person1 = new Person("Nike", 29, "teacher");
var person2 = new Person("Arvin", 20, "student");
```

5. 原型创建对象模式
```js
function Person() {}
Person.prototype.name = "Nike";
Person.prototype.age = 20;
Person.prototype.jbo = "teacher";
Person.prototype.sayName = function() {
  alert(this.name);
};
var person1 = new Person();
person1.sayName();
// 使用原型创建对象的方式，可以让所有对象实例共享它所包含的属性和方法
```

6. 组合使用构造函数模式和原型模式
```js
function Person(name, age, job) {
	this.name = name;
	this.age = age;
	this.job = job;
}
Person.prototype = {
	constructor: Person,
	sayName: function() {
		alert(this.name);
	};
}
var person1 = new Person('Nike', 20, 'teacher');
```

</details>

<b><details><summary>8. JavaScript 继承的方式</summary></b>

有六种，原型链继承、原型式继承、借用构造函数、寄生式继承、组合继承、寄生组合式继承

</details>

<b><details><summary>9. 什么是原型链</summary></b>

通过一个对象的 proto 可以找到它的原型对象，原型对象也是一个对象，就可以通过原型对象的 proto，最后找到了我们的 Object.prototype，从实例的原型对象开始一直到 Object.prototype 就是我们的原型链

</details>

<b><details><summary>10. JavaScript 数据类型</summary></b>

+ 基本数据类型：String、Number、Boolean、Null、Undefined、Symbol
+ 引用数据类型：Object、Array、Function

</details>

<b><details><summary>11. typeof 返回哪些数据类型</summary></b>

7种 分别为 string、boolean、number、object、function、undefined、symbol(ES6)

</details>

<b><details><summary>12. 一次 js 请求一般情况下有哪些地方会有缓存处理</summary></b>

dns 缓存、cdn 缓存、浏览器缓存、服务器缓存

</details>

<b><details><summary>13. 列举 3 种强制类型转换和 2 种隐式类型转换</summary></b>

+ 强制类型转换：parseInt、parseFloat、Number
+ 隐式类型转换：  +  -

</details>

<b><details><summary>14. 你对闭包的理解？优缺点？</summary></b>

+ 闭包就是能够读取其他函数内部变量的函数
+ 三大特性：
  - 函数嵌套函数
  - 函数内部可以引用外部的参数和变量
  - 参数和变量不会被垃圾回收机制回收

+ 优点：
  - 希望一个变量长期存储在内存中
  - 避免全局变量的污染
  - 私有成员的存在

+ 缺点：
 - 常驻内存，增加内存使用量
 - 使用不当会很容易造成内存泄露

```js
function outer() {
  var name = "rvean";
  function inner() {
    console.log(name);
  }
  return inner;
}
outer()(); // rvean

// 或者
function sayHi(name) {
  return () => {
    console.log(`Hi! ${name}`)
  }
}
sayHi("rve")() // Hi! rve
```

</details>

<b><details><summary>15. sort 排序原理</summary></b>

冒泡排序法，原理：比较相邻的元素。如果第一个比第二个大，就交换他们两个。对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。针对所有的元素重复以上的步骤，除了最后一个。持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```js
// 1. 升序
let arr1 = [45, 42, 10, 147, 7, 65, -74];
let result1 = arr1.sort(function (a, b) {
  return a - b;  // 若 return 返回值大于0(即a＞b),则a,b交换位置
});
console.log(result1); // [-74, 7, 10, 42, 45, 65, 147]

// 2. 降序
let arr2 = [45, 42, 10, 147, 7, 65, -74];
let result2 = arr2.sort(function (a, b) {
  return b - a;  // 若 return 返回值大于零(即b＞a),则a,b交换位置
});
console.log(result2); // [147, 65, 45, 42, 10, 7, -74]
```

</details>

<b><details><summary>16. for in 和 for of</summary></b>

+ for in
  - 一般用于遍历对象的可枚举属性，以及对象从构造函数原型中继承的属性。对于每个不同的属性，语句都会被执行
  - 不建议使用 for in 遍历数组，因为输出的顺序是不固定的
  - 如果迭代的对象的变量值是 null 或者 undefined, for in 不执行循环体，建议在使用 for in 循环之前，先检查该对象的值是不是 null 或者 undefined

+ for of
  - for of 语句在可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

```js
let obj = {
  a: 1,
  b: 2,
  c: 3
}
// for in
for (const k in obj) {
  console.log(k); //a b c
  console.log(obj[k]); //1 2 3
}
// for of    Object.keys(obj) => [a, b, c]
for (let k of Object.keys(obj)) {
  console.log(k); // a b c
  console.log(obj[k]); //1 2 3
}
```
</details>

<b><details><summary>17. 如何判断 JS 变量的类型</summary></b>

typeof、instanceof、 constructor、 prototype

</details>

<b><details><summary>18. for in、Object.keys 和 Object.getOwnPropertyNames 对属性遍历有什么区别</summary></b>

+ for in 会遍历自身及原型链上的可枚举属性
+ Object.keys 会将对象自身的可枚举属性的 key 输出
+ Object.getOwnPropertyNames 会将自身所有的属性的 key 输出

</details>

<b><details><summary>19. H5 与 Native 如何交互</summary></b>

通过 jsBridge

</details>

<b><details><summary>20. 如何判断一个对象是否为数组</summary></b>

1. 使用 instanceof 操作符
2. 使用 Array.isArray()方法
3. 使用 Object.prototype 上的原生 toString()方法判断

</details>

<b><details><summary>21.  defer 和 asnyc 属性的作用以及二者的区别</summary></b>

1. defer 和 async 的网络加载过程是一致的，都是异步执行
2. 区别在于加载完成之后什么时候执行，可以看出 defer 是文档所有元素解析完成之后才执行的
3. 如果存在多个 defer 脚本，那么它们是按照顺序执行脚本的，而 async，无论声明顺序如何，只要加载完成就立刻执行

+ script 标签存在两个属性，defer 和 async，这两个属性只对外部文件有效

</details>

<b><details><summary>22. 什么是面向对象</summary></b>

面向对象是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为

</details>

<b><details><summary>23. 你对松散类型的理解</summary></b>

JavaScript 中的变量为松散类型，所谓松散类型就是指当一个变量被申明出来就可以保存任意类型的值。
不像 SQL 一样申明某个键值为 int 就只能保存整型数值，申明 varchar 只能保存字符串。

</details>

<b><details><summary>24. JS 单线程还是多线程，如何显示异步操作</summary></b>

JS 本身是单线程的，他是依靠浏览器完成的异步操作

1. 主线程 执行 js 中所有的代码

2. 主线程 在执行过程中发现了需要异步的任务任务后扔给浏览器（浏览器创建多个线程执行），并在  callback queque  中创建对应的回调函数（回调函数是一个对象，包含该函数是否执行完毕等）

3. 主线程已经执行完毕所有同步代码。开始监听 callback queque， 一旦浏览器中某个线程任务完成将会改变回调函数的状态，主线程查看到某个函数的状态为已完成，就会执行该函数。

</details>

<b><details><summary>25. 数组函数 map/forEach/reduce/filter</summary></b>

1. map
```js
// 对数组进行遍历，返回新的数组，不改变原数组
let arr = [1, 2, 3, 4];
let arr2 = arr.map(function(val) {
  return val + 1;
});
console.log(arr) // [1, 2, 3, 4]
console.log(arr2) // [2, 3, 4, 5]
```

2. forEach
```js
// 遍历数组的每一项，不改变原数组
let arr = [1, 2, 3, 4];
arr.forEach(function(val) {
  console.log(val + 1); // 2, 3, 4, 5
});
console.log(arr) // [1, 2, 3, 4]
```

3. reduce
```js
// 对数组进行迭代，然后两两进行操作，最后返回一个值。返回值：return出来的结果
let arr = [1, 2, 3, 4];
let arr2 = arr.reduce(function(a, b) {
  return a * b;
});
console.log(arr2); // 1*2*3*4 = 24
console.log(arr); // [1, 2, 3, 4]
```

4. filter
```js
// 筛选一部分元素，返回值：一个满足筛选条件的新数组
let arr = [2, 5, 3, 4];
let ret = arr.filter(function(val) {
  return val > 3;
});
console.log(ret); // [5,4]
console.log(arr); // [2,5,3,4]
```

</details>

<b><details><summary>26. JS 作用域、块级作用域、变量提升</summary></b>

+ 作用域
  - 只会对某个范围产生作用，而不会对外产生影响的封闭空间。在这样的一些空间里，外部不能访问内部变量，但内部可以访问外部变量。
  - JS 中作用域有：全局作用域、函数作用域。ES6 中新增了 块级作用域。

+ 作用域的分类
  - 块作用域 花括号 {} ，if 语句和 for 语句里面的 {} 也属于块作用域
  - 词法作用域/函数作用域（js 属于词法作用域） 作用域只跟在何处被创建有关系，跟在何处被调用没有关系
  - 动态作用域 作用域只跟在何处被调用有关系，跟在何处被创建没有关系

+ 变量提升
  - 所有申明都会被提升到作用域的最顶上
  - 函数声明的优先级优于变量申明，且函数声明会连带定义一起被提升
  - var 关键字和 function 关键字声明的变量会进行变量提升

</details>

<b><details><summary>27. var、let、const 的区别</summary></b>

+ var 定义的变量，没有块的概念，可以跨块访问, 不能跨函数访问

+ let 定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问

+ const 用来定义常量，使用时必须初始化(即必须赋值)，只能在块作用域里访问，而且不能修改

</details>

<b><details><summary>28. null 和 undefined 的区别</summary></b>

+ null： Null 类型，代表“空值"，代表一个空对象指针，使用 typeof 运算得到 “object"，所以你可以认为它是一个特殊的对象值
+ undefined： Undefined 类型，当一个声明了一个变量未初始化时，得到的就是 undefined

</details>

<b><details><summary>29. JS 哪些操作会造成内存泄露</summary></b>

+ 意外的全局变量引起的内存泄露
+ 闭包引起的内存泄露
+ 没有清理的 DOM 元素引用
+ 被遗忘的定时器或者回调
+ 子元素存在引起的内存泄露

1. JS 的垃圾回收机制：找出不再使用的变量，然后释放掉其占用的内存，但是这个过程不是实时的，因为其开销比较大，所以垃圾回收系统（GC）会按照固定的时间间隔,周期性的执行
2. 标记清除，JS 中最常用的垃圾回收方式就是标记清除。当变量进入环境时，例如，在函数中声明一个变量，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其标记为“离开环境”。

> 怎样避免内存泄露
+ 减少不必要的全局变量，或者生命周期较长的对象，及时对无用的数据进行垃圾回收
+ 注意程序逻辑，避免“死循环”之类
+ 避免创建过多的对象 原则：不用了的东西要及时归还

</details>

<b><details><summary>30. 重排与重绘的区别，什么情况下会触发</summary></b>

1. 重排：浏览器下载完页面中的所有组件（HTML、JavaScript、CSS、图片）之后会解析生成两个内部数据结构（DOM 树和渲染树），DOM 树表示页面结构，渲染树表示 DOM 节点如何显示。重排是 DOM 元素的几何属性变化，DOM 树的结构变化，渲染树需要重新计算。
2. 重绘：重绘是一个元素外观的改变所触发的浏览器行为，例如改变 visibility、outline、背景色等属性。浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。由于浏览器的流布局，对渲染树的计算通常只需要遍历一次就可以完成。但 table 及其内部元素除外，它可能需要多次计算才能确定好其在渲染树中节点的属性值，比同等元素要多花两倍时间，这就是我们尽量避免使用 table 布局页面的原因之一。
3. 简述重绘和重排的关系：重绘不会引起重排，但重排一定会引起重绘，一个元素的重排通常会带来一系列的反应，甚至触发整个文档的重排和重绘，性能代价是高昂的。
4. 什么情况下会触发重排？
  + 页面渲染初始化时
  + 浏览器窗口改变尺寸
  + 元素尺寸、位置、内容改变时
  + 添加或删除可见的 DOM 元素时

5. 重排优化方法
  + 将多次改变样式属性的操作合并成一次操作，减少 DOM 操作数
  + 如果要批量添加 DOM，可以先让元素脱离文档流，操作完后再带入文档流，这样只会触发一次重排
  + 将需要多次重排的元素，position 属性设为 absolute 或 fixed，这样此元素就脱离了文档流，它的变化不会影响到其他元素。例如有动画效果的元素就最好设置为绝对定位。
  + 由于 display 属性为 none 的元素不在渲染树中，对隐藏的元素操作不会引发其他元素的重排。如果要对一个元素进行复杂的操作时，可以先隐藏它，操作完成后再显示。这样只在隐藏和显示时触发两次重排。
  + 在内存中多次操作节点，完成后再添加到文档中去。例如要异步获取表格数据，渲染到页面。可以先取得数据后在内存中构建整个表格的 html 片段，再一次性添加到文档中去，而不是循环添加每一行。

</details>

<b><details><summary>31. 事件绑定与普通事件有什么区别</summary></b>

+ 用普通事件添加相同事件，下面会覆盖上面的，而事件绑定不会
+ 普通事件是针对非 dom 元素，事件绑定是针对 dom 元素的事件

</details>

<b><details><summary>32. call 、 apply、bind 的含义和区别</summary></b>

+ call：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.call(A, args1,args2);即 A 对象调用 B 对象的方法
+ apply：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即 A 对象应用 B 对象的方法
+ call 和 apply 其实是一样的，区别就在于传参时参数是一个一个传或者是以一个数组的方式来传
+ call 和 apply 都是在调用时生效，改变调用者的 this 指向
+ bind 也是改变 this 指向，不过不是在调用时生效，而是返回一个新函数

```js
const obj = {
  name: 'Tom'
}
function sayHi() {
  console.log('Hi! ' + this.name)
}

// call
sayHi.call(obj) // Hi! Tom

// bind
const newFunc = sayHi.bind(obj)
newFunc() // Hi! Tom
```

+ call 和 apply 的应用

```js
// 比如求数组的最大值 Math.max.apply(this, 数组)
let arr = [5, 458, 120, -215];
let maxNum = Math.max.apply(this, arr);
console.log(maxNum); // 458

let maxNumber = Math.max.call(this, 5, 458, 120, -215);
console.log(maxNumber); // 458
```

</details>

<b><details><summary>33. 如何判断一个对象是否属于某个类</summary></b>

```js
console.log(a instanceof Person)
```

</details>

<b><details><summary>34. new 操作符具体干了什么</summary></b>

```js
function Test() {}
const test = new Test()

// 1. 创建一个新对象
const obj = {}
// 2. 设置新对象的 constructor 属性为构造函数的名称，设置新对象的 __proto__ 属性指向构造函数的 prototype 对象
obj.constructor = Test
obj.__proto__ = Test.prototype
// 3. 使用新对象调用函数，函数中的 this 被指向新实例对象
Test.call(obj)
// 4. 将初始化完毕的新对象地址，保存到等号左边的变量中
```

</details>

<b><details><summary>35. 数组 Array 常用方法</summary></b>

+ Array.map()
```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.map(val => val * 2);
console.log(newArr) // [2, 4, 6, 8, 10]
```

+ Array.forEach()  遍历数组
```js
arr.forEach(val => val * 2);
```

+ Array.filter()  检测数值元素，并返回符合条件所有元素的数组
```js
let res1 = arr.filter(val => {
  return val > 3
})
console.log(res1) // [4, 5]
```

+ Array.every()
```js
// 检测数值元素的每个元素是否都符合条件,如果有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测
let res2 = arr.every(val => {
  return val > 3
})
console.log(res2) // false
```

+ Array.some()
```js
// 检测数组元素中是否有元素符合指定条件,如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测
let res3 = arr.some(val => {
  return val > 3
})
console.log(res3) // true
```

+ Array.reduce()
```js
// 接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值
let res4 = arr.reduce((a, b) => {
  return a + b
})
console.log(res4) // 15
```

+ Array.push()  向数组的末尾添加元素
+ Array.pop()   删除并返回数组的最后一个元素
+ Array.unshift()  向数组的开头添加元素
+ Array.shift()  删除并返回数组的第一个元素
+ Array.isArray()  判断一个对象是不是数组，返回的是布尔值
+ Array.concat()  连接两个或更多的数组，并返回结果
+ Array.toString()  把数组转换为字符串，并返回结果
+ Array.join()  把数组转换为字符串，元素是通过指定的分隔符进行分隔的
+ Array.splice()  添加或删除数组中的元素，会改变原始数组
```js
arr.splice(2, 0, 9)  // [1, 2, 9, 3, 4, 5]，添加
arr.splice(2, 1)  // [1, 2, 4, 5]，删除
arr.splice(2, 1, 7)  // [1, 2, 7, 4, 5]，替换
```

</details>

<b><details><summary>36. 字符串 String 常用方法</summary></b>

+ String.concat()  连接字符串
+ String.indexOf()  返回某个元素在字符串中首次出现的位置
+ String.lastIndexOf()  从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置
+ String.match()  查找找到一个或多个正则表达式的匹配
+ String.replace()  在字符串中查找匹配的子串， 并替换与正则表达式匹配的子串
+ String.search()  查找与正则表达式相匹配的值
+ String.slice()  提取字符串的片断，并在新的字符串中返回被提取的部分
+ String.split()  把字符串分割为字符串数组
+ String.substr()  从起始索引号提取字符串中指定数目的字符
+ String.substring()  提取字符串中两个指定的索引号之间的字符
+ String.toLowerCase()  把字符串转换为小写
+ String.toUpperCase()  把字符串转换为大写
+ String.trim()  删除字符串的头尾空格

</details>

<b><details><summary>37. target 和 currentTarget 区别</summary></b>

+ event.target  返回触发事件的元素
+ event.currentTarget  返回绑定事件的元素

</details>

<b><details><summary>38. 使用构造函数的注意点</summary></b>

+ 首字母需要大写，需要跟new关键字进行搭配使用，创建一个新的实例
+ 在构造函数内部通过this+属性名的形式为实例添加一些属性和方法
+ 构造函数一般不需要返回值，如果有返回值
  - 如果返回值是一个基本数据类型，那么调用构造函数，返回值仍旧是那么创建出来的对象
  - 如果返回值是一个复杂数据类型，那么调用构造函数的时候，返回值就是这个return之后的那个复杂数据类型

</details>

<b><details><summary>39. 自执行函数?用于什么场景？好处?</summary></b>

+ 自执行函数：声明一个匿名函数，马上调用这个匿名函数
+ 作用：创建一个独立的作用域

+ 好处：防止变量弥散到全局，以免各种 js 库冲突。隔离作用域避免污染，或者截断作用域链，避免闭包造成引用变量无法释放。利用立即执行特性，返回需要的业务函数或对象，避免每次通过条件判断来处理

+ 场景：一般用于框架、插件等场景

</details>

<b><details><summary>40. 多个页面之间如何进行通信</summary></b>

+ cookie
+ localeStorage 和 sessionStorage
+ web worker

</details>

<b><details><summary>41. 如何做到修改 url 参数页面不刷新</summary></b>

HTML5 引入了 history.pushState() 和 history.replaceState() 方法，它们分别可以添加和修改历史记录条目
```js
let states = {
  foo: "bar"
};

history.pushState(states, "标题", "bar.html");
```

</details>

<b><details><summary>42. 如何阻止冒泡与默认行为</summary></b>

+ 阻止冒泡行为：`event.stopPropagation()`
+ 阻止默认行为：`event.preventDefault()`

</details>

<b><details><summary>43. JavaScript 的同源策略</summary></b>

+ 同源策略：一段脚本只能读取来自于同一来源的窗口和文档的属性
  - 源包括三个部分：协议、域名、端口（http 协议的默认端口是 80）。如果有任何一个部分不同，则源不同，那就是 跨域。
  - 限制：这个源的文档没有权利去操作另一个源的文档。这个限制体现在：
    - Cookie、LocalStorage 和 IndexDB 无法获取
    - 无法获取和操作 DOM
    - 不能发送 Ajax 请求。Ajax 只适合同源的通信
    - Ajax 在不同域名下的请求无法实现，需要进行跨域操作

</details>

<b><details><summary>44. a = a || b，这行代码是什么意思，作用</summary></b>

+ 这种写法称为 短路表达式，常用于函数参数的空判断

```js
// 相当于
let a
if (a) {
  a = a
} else {
  a = b
}
```

</details>

<b><details><summary>45. 复杂数据类型如何转变为字符串</summary></b>

+ 首先调用 valueOf 方法，如果方法的返回值是一个基本数据类型，就返回这个值
+ 如果调用 valueOf 方法之后的返回值仍旧是一个复杂数据类型，就会调用该对象的 toString 方法
+ 如果 toString 方法调用之后的返回值是一个基本数据类型，就返回这个值
+ 如果 toString 方法调用之后的返回值是一个复杂数据类型，就报一个错误

</details>

<b><details><summary>46. this 的指向问题</summary></b>

+ 全局环境、普通函数（非严格模式）指向 window
+ 普通函数（严格模式）指向 undefined
+ 函数作为对象方法及原型链指向的就是上一级的对象
+ 构造函数指向构造的对象
+ DOM 事件中指向触发事件的元素
+ 箭头函数没有自己的 this，而是使用箭头函数所在的作用域的 this，即指向箭头函数定义时（而不是运行时）所在的作用域

</details>

<b><details><summary>47. 正则表达式构造函数 new RegExp() 与正则表达式字面量 // 有什么不同</summary></b>

使用正则表达字面量的效率更高、显得更加简短

</details>

<b><details><summary>48. caller 与 callee 的作用</summary></b>

+ caller 返回一个调用当前函数的引用。如果是由顶层调用的话，则返回 null
```js
var callerTest = function() {
  console.log(callerTest.caller);
};
function a() {
  callerTest();
}
a(); // 输出function a() {callerTest();}
callerTest(); // 输出null
```

+ callee 返回一个正在被执行函数的引用，callee 是 arguments 对象的一个成员 表示对函数对象本身的引用
```js
var c = function(x, y) {
  console.log(arguments.length, arguments.callee.length, arguments.callee);
};
c(1, 2, 3); //输出3 2 function(x,y) {console.log(arguments.length,arguments.callee.length,arguments.callee)}
```

</details>

<b><details><summary>49. 异步加载 js 的方法</summary></b>

+ `<script></script>` 标签的 async="async" 属性
+ `<script></script>` 标签的 defer="defer" 属性
+ 动态创建 `<script></script>` 标签
```js
(function() {
  var s = document.createElement_x("script");
  s.src = "http://code.jquery.com/jquery-1.7.2.min.js";
  var tmp = document.getElementsByTagName_r("script")[0];
  tmp.parentNode.insertBefore(s, tmp);
})();
```

+ Ajax eval（使用 Ajax 得到脚本内容，然后通过 eval_r(xmlhttp.responseText)来运行脚本）
+ iframe 方式

</details>

<b><details><summary>50. 去除数组重复成员的方法</summary></b>

```js
let arr = [1, 2, 2, 3, 4, 5, 5]

// 1. 扩展运算符 + new Set  Set 对象存储的值总是唯一的
[...new Set(arr)]

// 2. Array.from + new Set
function dedupe(arr) {
  return Array.from(new Set(arr));
}
dedupe(arr);

// 3. forEach
function unique(arry) {
  const temp = [];
  arry.forEach(e => {
    if (temp.indexOf(e) == -1) {
      temp.push(e);
    }
  });

  return temp;
}
```

</details>

<b><details><summary>51. 去除字符串里面的重复字符</summary></b>

```js
[...new Set("ababbc")].join('')
```

</details>

<b><details><summary>52. 求数组的最大值、最小值</summary></b>

```js
let arr = [1, 2, 1, 3, 4, 5, 5]
let max = Math.max.apply(null, arr) // 最大值
let min = Math.min.apply(null, arr) // 最小值
```

</details>

<b><details><summary>53. 文档碎片的理解和使用</summary></b>

+ 文档碎片：`document.createDocumentFragment()` ，一个容器，用于暂时存放创建的dom元素
+ 作用：将需要添加的大量元素，先添加到文档碎片中，再将文档碎片添加到需要插入的位置，大大减少dom操作，提高性能

```js
// 普通方式：（操作了100次dom）
for (var i = 100; i > 0; i--) {
  var elem = document.createElement("div");
  document.body.appendChild(elem); // 放到body中
}

//  文档碎片：(操作1次dom)
var df = document.createDocumentFragment();
for (var i = 100; i > 0; i--) {
  var elem = document.createElement("div");
  df.appendChild(elem);
}
document.body.appendChild(df); //最后放入到页面上
```

</details>

<b><details><summary>54. 什么是原型、原型的作用</summary></b>

+ 原型：实例在被创建的那一刻，构造函数的 prototype 属性的值
+ 作用：实现资源共享

</details>

<b><details><summary>55. JavaScript 的继承怎么实现，如何避免原型链上面的对象共享</summary></b>

+ 用构造函数和原型链的混合模式去实现继承
+ 避免对象共享可以参考经典的 extend()函数，很多前端框架都有封装的，就是用一个空函数当做中间变量


</details>

<b><details><summary>56. 说说你对作用域链的理解</summary></b>

作用域链的作用：保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到 window 对象即被终止，作用域链向下访问变量是不被允许的

</details>

<b><details><summary>57. 说说你对作用域链的理解</summary></b>

作用域链的作用：保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到 window 对象即被终止，作用域链向下访问变量是不被允许的

</details>

<b><details><summary>58. JavaScript 原型，原型链 ? 有什么特点？</summary></b>

+ 原型对象也是普通的对象，是对象一个自带隐式的__proto__属性，原型也有可能有自己的原型，如果一个原型对象的原型不为 null 的话，我们就称之为原型链
+ 原型链是由一些用来继承和共享属性的对象组成的（有限的）对象链
+ 当我们需要一个属性的时，Javascript 引擎会先看当前对象中是否有这个属性， 如果没有的话，就会查找他的 Prototype 对象是否有这个属性

</details>

<b><details><summary>59. eval 是做什么的</summary></b>

+ 它的功能是把对应的字符串解析成 JS 代码并运行
+ 应该避免使用 eval，不安全，非常耗性能（2 次，一次解析成 js 语句，一次执行）

</details>

<b><details><summary>60. 快速的让一个数组乱序</summary></b>

```js
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
let arr2 = arr.sort(() => 0.5 - Math.random())
```

</details>

<b><details><summary>61. js 中哪些会被隐式转换为 false</summary></b>

undefined、null、关键字 false、NaN、零、空字符串

</details>

<b><details><summary>62. 列举浏览器对象模型 BOM 里常用的对象，并列举 window 对象的常用方法</summary></b>

+ 对象：window，document，location，screen，history，navigator
+ 方法：alert()，confirm()，prompt()，open()，close()

</details>

<b><details><summary>63. 定时器 setInterval 有一个有名函数 fn1，setInterval(fn1, 500) 与 setInterval(fn1(), 500) 有什么区别</summary></b>

+ 第一个是重复执行每 500 毫秒执行一次，后面一个只执行一次

</details>

<b><details><summary>64. 你用过 require.js 吗？它有什么特性？</summary></b>

+ 实现 js 文件的异步加载，避免网页失去响应
+ 管理模块之间的依赖性，便于代码的编写和维护

+ 核心原理：核心是 js 的加载模块，通过正则匹配模块以及模块的依赖关系，保证文件加载的先后顺序，根据文件的路径对加载过的文件做了缓存

+ 让你自己设计实现一个 requireJS，你会怎么做
  - 核心是实现 js 的加载模块，维护 js 的依赖关系，控制好文件加载的先后顺序

</details>

<b><details><summary>65. 对象浅拷贝和深拷贝有什么区别</summary></b>

+ 在 JS 中，除了基本数据类型，还存在对象、数组这种引用类型。基本数据类型的拷贝是直接拷贝变量的值，而引用类型拷贝的其实是变量的地址

```js
let o1 = {a: 1}
let o2 = o1

// 在这种情况下，如果改变 o1 或 o2 其中一个值的话，另一个也会变，因为它们都指向同一个地址
o2.a = 3
console.log(o1.a) // 3
```

+ 浅拷贝和深拷贝就是在这个基础之上做的区分，如果在拷贝这个对象的时候，只对基本数据类型进行了拷贝，而对引用数据类型只是进行了引用的传递，而没有重新创建一个新的对象，则认为是浅拷贝。反之，在对引用数据类型进行拷贝的时候，创建了一个新的对象，并且复制其内的成员变量，则认为是深拷贝

</details>

<b><details><summary>66. JS 怎么实现一个类。怎么实例化这个类</summary></b>

严格来讲 js 中并没有类的概念，不过 js 中的函数可以作为 构造函数 来使用，通过 new 来实例化，其实函数本身也是一个对象。

</details>

<b><details><summary>67. Javascript 中，有一个函数，执行对象查找时，永远不会去查找原型，这个函数是</summary></b>

hasOwnProperty

</details>

<b><details><summary>68. 简述创建函数的几种方式</summary></b>

+ 函数声明
```js
function sum1(a, b) {
  return a + b
}
```

+ 函数表达式
```js
var sum2 = function(a, b) {
  return a + b;
}
```

+ 函数对象方式
```js
var sum3 = new Function("a", "b", "return a + b")
```

</details>

<b><details><summary>69. window.location 的方法</summary></b>

+ `window.location.search()` ，查询(参数)部分，返回值：?ver=1.0&id=id1 也就是问号后面的
+ `window.location.hash`  ，锚点，返回值：#home 
+ `window.location.reload()` ，刷新当前页面

</details>

<b><details><summary>70. 事件绑定的方式</summary></b>

1. 嵌入 dom  `<button onclick="func()">按钮</button>`
2. 直接绑定  `btn.onclick = function() {}`
3. 事件监听  `btn.addEventListener("click", function() {})`

</details>

<b><details><summary>71. 事件循环</summary></b>

事件循环是一个单线程循环，用于监视调用堆栈并检查是否有工作即将在任务队列中完成。如果调用堆栈为空并且任务队列中有回调函数，则将回调函数出队并推送到调用堆栈中执行

</details>

<b><details><summary>72. 事件模型</summary></b>

+ DOM0 
```js
// 直接绑定
<button onclick="func()">按钮</button>

btn.onclick = function() {}
btn.onclick = null
```

+ DOM2
```js
// DOM2 级事件可以冒泡和捕获
// 绑定
btn.addEventListener('click', func)
// 解绑
btn.removeEventListener('click', func)
```

+ DOM3 - DOM3 级事件在 DOM2 级事件的基础上添加了更多的事件类型
  - UI事件，当用户与页面上的元素交互时触发，如：load、scroll
  - 焦点事件，当元素获得或失去焦点时触发，如：blur、focus
  - 鼠标事件，当用户通过鼠标在页面执行操作时触发如：dbclick、mouseup
  - 滚轮事件，当使用鼠标滚轮或类似设备时触发，如：mousewheel
  - 文本事件，当在文档中输入文本时触发，如：textInput
  - 键盘事件，当用户通过键盘在页面上执行操作时触发，如：keydown、keypress
  - 合成事件，当为IME（输入法编辑器）输入字符时触发，如：compositionstart
  - 变动事件，当底层DOM结构发生变化时触发，如：DOMsubtreeModified

</details>

<b><details><summary>73. 如何自定义事件</summary></b>

+ 原生提供了 3 个方法实现自定义事件:
  - createEvent，设置事件类型，是 html 事件 还是 鼠标事件
  - initEvent 初始化事件，事件名称，是否允许冒泡，是否阻止自定义事件
  - dispatchEvent 触发事件

</details>

<b><details><summary>74. prototype 和 proto 的关系是什么</summary></b>

+ 所有的对象都拥有 proto 属性，它指向对象构造函数的 prototype 属性
```js
let obj = {}
obj.__proto__ === Object.prototype // true

function Test(){}
test.__proto__ == Test.prototype // true
```

+ 所有的函数都同时拥有 proto 和 protytpe 属性，函数的 proto 指向自己的函数实现，函数的 protytpe 是一个对象，所以函数的 prototype 也有 proto 属性，指向 Object.prototype
```js
function func() {}
func.prototype.__proto__ === Object.prototype // true

Object.prototype.__proto__ // null
```

</details>

<b><details><summary>75. 说说你对 promise 的了解</summary></b>

Promise 是异步编程的一种解决方案。
Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
Promise 是一个对象，从它可以获取异步操作的消息。

Promise 对象有以下两个特点
  - 对象的状态不受外界影响，Promise 对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）
  - 一旦状态改变，就不会再变，任何时候都可以得到这个结果

</details>

<b><details><summary>76. 箭头函数需要注意的地方</summary></b>

+ 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象，用call apply bind也不能改变this指向
+ 不可以当作构造函数，也就是说，不可以使用 new 命令
+ 不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替
+ 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数
+ 箭头函数没有原型对象prototype

```js
function foo() {
  setTimeout(() => {
    console.log("id:", this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 }); // id: 42
```

</details>

<b><details><summary>77. ES6 如何动态加载 import</summary></b>

```js
import("lodash").then(_ => {
  // Do something with lodash (a.k.a '_')...
});
```

</details>

<b><details><summary>78. ES6 中类的定义</summary></b>

```js
// 1、类的基本定义
class Parent {
  constructor(name = "小白") {
    this.name = name;
  }
}

// 2、生成一个实例
let g_parent = new Parent();
let v_parent = new Parent("v");

// 3、继承
class Child extends Parent {}
```

</details>
