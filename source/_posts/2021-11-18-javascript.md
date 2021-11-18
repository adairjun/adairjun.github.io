---
title: 快速掌握一门语言常用的50% - javascript
date: 2021-11-18 00:25:25
categories: javascript
---

## 了解该语言的基本数据类型，基本语法和主要语言构造；主要数学运算符和print函数的使用，达到能够写课后习题水平；

print函数: 一共有4种

```javascript
window.alert("this is window.alert");

document.getElementById("demo").innerHTML = "we can use innerHTML to modify the demo id";

document.write("we can also use write function to write to html");

console.log("we can also print it to console");
```

基本语法：

变量使用let, const
```javascript
let i = 5  // number
let j = "this is string" // string
let k = [1,2,3,4,5] // array

let myMap = new Map();     // map
let keyString = "key"; 
 
myMap.set(keyString, "value");
 
myMap.get(keyString);    // "value"
myMap.get("key");   // "value" 因为 keyString === 'key'

let h = {
    "first": "1",
    "second": "2"
}                  // object

let m = () => {
    console.log("this is function")
}                 // function

class Example {
    constructor(a) {
        this.a = a;
    }
}             // class

let example = new Example();  // class
```

算术操作符，和C语言一样：
```javascript
let z = (5 + 6) * 10
```

javascript的数据类型: 因为将16从number转换成为了string

```javascript
16 + "Volvo"

//output is:
"16Volvo"
```

## 其次掌握数组和其他集合类的使用，有基础的话可以理解一下泛型，如果理解不了也问题不大，后面可以补；

将string转换为number：
```javascript
// 不指定进制时默认为 10 进制
Number.parseInt('12.34'); // 12
Number.parseInt(12.34);   // 12

// 用于把一个字符串解析成浮点数。
Number.parseFloat('123.45')    // 123.45
Number.parseFloat('123.45abc') // 123.45
// 无法被解析成浮点数，则返回 NaN
Number.parseFloat('abc') // NaN

// 用于判断给定的参数是否为整数。
Number.isInteger(value)
Number.isInteger(0); // true
// JavaScript 内部，整数和浮点数采用的是同样的储存方法,因此 1 与 1.0 被视为相同的值
Number.isInteger(1);   // true
Number.isInteger(1.0); // true
 
Number.isInteger(1.1);     // false
Number.isInteger(Math.PI); // false
```

math对象需要掌握的方法：
```javascript

//用于返回数字的整数部分。
Math.trunc(12.3); // 12
Math.trunc(12);   // 12
 
// 整数部分为 0 时也会判断符号
Math.trunc(-0.5); // -0
Math.trunc(0.5);  // 0
 
// Math.trunc 会将非数值转为数值再进行处理
Math.trunc("12.3"); // 12
 
// 空值或无法转化为数值时时返回 NaN
Math.trunc();           // NaN
Math.trunc(NaN);        // NaN
Math.trunc("hhh");      // NaN
Math.trunc("123.2hhh"); // NaN

Math.random() // 返回 0 ~ 1 之间的随机数
Math.floor() // 对 x 进行下舍入
Math.floor(Math.random()* 100); // 结合两者可以返回 0 ~ 100 之间的随机数
```

string需要掌握的方法:
```javascript
// javascript 自带length方法
let txt = "Hello World!";
let len = txt.length;

// substring
let str="Hello world!";
console.log(str.substring(3)+"<br>");
console.log(str.substring(3,7));

// includes 检测是否包含字符串
let string = "apple,banana,orange";
string.includes("banana");     // true

// 字符串使用 indexOf() 来定位字符串中某一个指定的字符首次出现的位置：
let str="Hello world, welcome to the universe.";
let n=str.indexOf("welcome");

// replace将执行一次替换，当第一个 "Microsoft" 被找到，它就被替换为 "Runoob"：
let str="Visit Microsoft! Visit Microsoft!";
let n=str.replace("Microsoft","Runoob");

// 执行一个全局替换:
let str="Mr Blue has a blue house and a blue car";
let n=str.replace(/blue/g,"red");
```

数组需要掌握的方法:
```javascript
// javascript 自带length方法
let fruits = ["Banana", "Orange", "Apple", "Mango"];
let len = fruits.length;

// 数组是否包含指定值
// 参数1：包含的指定值
[1, 2, 3].includes(1);    // true
 
// 参数2：可选，搜索的起始索引，默认为0
[1, 2, 3].includes(1, 2); // false
 
// NaN 的包含判断
[1, NaN, 3].includes(NaN); // true

// append
fruits.push("Hola");

// 迭代
let myStringArray = ["Hello","World"];
let arrayLength = myStringArray.length;
for (let i = 0; i < arrayLength; i++) {
    console.log(myStringArray[i]);
    //Do something
}

// foreach
let numbers = [4, 9, 16, 25];
function myFunction(item, index) {
   console.log("item is "+ item + ", index is" + index);
}
numbers.forEach(myFunction)

// for of
let colors = ['red', 'green', 'blue'];
for (const color of colors){
    console.log(color);
}
```

map需要掌握的方法:
```javascript
// 迭代 

// for each 很少用
let myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 logs。 一个是 "0 = zero" 另一个是 "1 = one"
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
}, myMap)


//使用 for of
let myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 log。 一个是 "0 = zero" 另一个是 "1 = one"
for (let [key, value] of myMap) {
  console.log(key + " = " + value);
}
for (let [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
/* 这个 entries 方法返回一个新的 Iterator 对象，它按插入顺序包含了 Map 对象中每个元素的 [key, value] 数组。 */
 
// 将会显示两个log。 一个是 "0" 另一个是 "1"
for (let key of myMap.keys()) {
  console.log(key);
}
/* 这个 keys 方法返回一个新的 Iterator 对象， 它按插入顺序包含了 Map 对象中每个元素的键。 */
 
// 将会显示两个log。 一个是 "zero" 另一个是 "one"
for (let value of myMap.values()) {
  console.log(value);
}

// check whether element is existed in the map or not
if (myMap.get("key") === undefined) {
  
}

```


## 简单字符串处理。所谓简单，就是Regex和Parser以下的内容，什么查找替换，截断去字串之类的。不过这个阶段有一个难点，就是字符编码问题。如果理解不了，可以先跳过，否则的话最好在这时候把这个问题搞定，免留后患；

```javascript
上面已经写了 string的replace方法
```

## 基本面向对象或者函数式编程的特征，无非是什么继承、多态、Lambda函数之类的，如果有经验的话很快就明白了；

```javascript
在 JavaScript 的现实场景中，尤其是前端代码，我们很少真正用到类继承，大多数时候，工厂函数就能完成我们的目标。

以React为例，官方这几年推崇 Hooks 的意图也很明显 —— 摆脱JavaScript class 带来的复杂性，拥抱函数式风格。

由于 JavaScript 实现的特殊性，在 JavaScript 应用中使用 class 对于一些程序员来说有许多坑，于此同时，大多数场景下其他替代方案如 工厂函数 可能更契合JavaScript的特性，反而带来更好的效果。

当然，并不是一杆子打死 JavaScript 的 class，在一些特别适合 OOP 的场景中，依然鼓励使用 class 。
```

```javascript
//javascript 不会使用大量class，只需要掌握继承即可
class Point {
   constructor(x, y) {
      this.x = x;
      this.y = y;
   }
   
   toString() {
       return x.toString() + ' ' + y.toString();
   }
}

class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}

```

```javascript
// javascript function 的 this

function ListNode(val) {
         this.val = (val===undefined ? 0 : val)
}

// 如果想要使用val的话，需要使用new，把这个funciton绑定到一个object上
let node1 = new ListNode(1);
console.log(node1.val);

```

## 异常、错误处理、断言、日志和调试支持，对单元测试的支持。你不一定要用TDD，但是在这个时候应该掌握在这个语言里做TDD的基本技能；

```javascript
nodejs 语言里面没有自带unit test，但是可以使用Test Framework，
可以使用Jest
https://www.testim.io/blog/jest-testing-a-helpful-introductory-tutorial/

```

## 程序代码和可执行代码的组织机制，运行时模块加载、符号查找机制，这是初学时的一个难点，因为大部分书都不太注意介绍这个极为重要的内容

```javascript
使用任何语言进行编程都有一个类似的问题，那就是如何组织代码，具体来说，如何避免命名冲突？如何合理组织各种源文件？如何使用第三方库？各种代码和依赖库如何编译连接为一个完整的程序？

比如java是使用包的机制

但是JavaScript是使用module，

```

一个模块就是一个独立的文件, 该文件内部的所有变量，外部无法获取。
```javascript
let firstName = 'Michael';
let lastName = 'Jackson';
let year = 1958;

// export 一定要有花括号, 一般放在文件的末尾
export { firstName, lastName, year };
```


使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。
```javascript
// ES6模块

import { firstName, lastName, year } from './profile.js';
import { lastName as surname } from './profile.js'; // 如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的变量重命名。

import { stat, exists, readFile } from 'fs'; // fs是模块文件名，由于不带有路径，必须通过配置，告诉引擎怎么取到这个模块。

import * as circle from './circle'; // 整体加载

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

nodejs如果要开启import的语法，需要在package.json里面加上这一句
```javascript
{
  "type": "module"
}
```

## 基本输入输出和文件处理，输入输出流类的组织，这通常是比较繁琐的一部分，可以提纲挈领学一下，搞清楚概念，用到的时候查就是了。到这个阶段可以写大部分控制台应用了

nodejs 命令行输入
```javascript
// 从命令行获取参数值的方法是使用 Node.js 中内置的 process 对象

// 它公开了 argv 属性，该属性是一个包含所有命令行调用参数的数组。
//第一个参数是 node 命令的完整路径。
// 第二个参数是正被执行的文件的完整路径。
// 所有其他的参数从第三个位置开始。
// 比如：node app.js joe

process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`)
})
```

Node.js 提供一组类似 UNIX（POSIX）标准的文件操作API。 Node 导入文件系统模块(fs)语法如下所示：
```javascript
// 利用fs包进行文件的输入输出的处理
import * as fs from "fs" 

// 异步读取
fs.readFile('input.txt', function (err, data) {
   if (err) {
       return console.error(err);
   }
   console.log("异步读取: " + data.toString());
});

// 同步读取
let data = fs.readFileSync('input.txt');
console.log("同步读取: " + data.toString());

console.log("程序执行完毕。");

fs.writeFile('input.txt', '我是通 过fs.writeFile 写入文件的内容',  function(err) {
   if (err) {
       return console.error(err);
   }
   console.log("数据写入成功！");
});
```

## 该语言如何进行callback方法调用，如何支持事件驱动编程模型。在现代编程环境下，这个问题是涉及开发思想的一个核心问题，几乎每种语言在这里都会用足功夫，.NET的delegate，Java的anonymous inner class，Java 7的closure，C++OX的 tr1::function/bind，五花八门。如果能彻底理解这个问题，不但程序就不至于写得太走样，而且对该语言的设计思路也能有比较好的认识；

```javascript
// Nodejs 所有 API 都支持回调函数

// Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。

// Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。
// Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.
```

通过promise来avoid callback hell

```javascript
// 其实这个promise 并不是说要自己创建一个promise对象，而是说有很多API已经使用了promise，只要能读懂就行了
import { readdir } from 'fs/promises';

try {
  const files = await readdir(path);  // await 是等待readdir完成，因为readdir是异步的
  for (const file of files)
    console.log(file);
} catch (err) {
  console.error(err);
}


```

事件驱动模型,尽管Node.js 有多个内置的事件，但是如果想要自定义事件，那么可以使用EventEmitter

```javascript
// 引入 events 模块
import * as events from "events"

// 创建 eventEmitter 对象
let eventEmitter = new events.EventEmitter();
 
// 创建事件处理程序
let connectHandler = () => {
   console.log('连接成功。');
  
   // 触发 data_received 事件 
   eventEmitter.emit('data_received');
}
 
// 绑定 connection 事件处理程序
eventEmitter.on('connection', connectHandler);
 
// 使用匿名函数绑定 data_received 事件
eventEmitter.on('data_received', function(){
   console.log('数据接收成功。');
});
 
// 触发 connection 事件 
eventEmitter.emit('connection');
 
console.log("程序执行完毕。");
```


## 如果有必要，可在这时研究regex和XML处理问题，如无必要可跳过；

```javascript
//regex 已经学习过了
```

## 序列化和反序列化，掌握一下缺省的机制就可以了；

```javascript
// 序列化成为JSON
class MyClass {
  constructor() {
    this.foo = 3
  }
}

let myClass = new MyClass()
let json = JSON.stringify(myClass);

// 反序列化
let newMyClass = JSON.parse(json);

```


## 如果必要，可了解一下线程、并发和异步调用机制，主要是为了读懂别人的代码，如果自己要写这类代码，必须专门花时间严肃认真系统地学习，严禁半桶水上阵

```javascript
//nodejs 是单线程，无并发，
// 语言本身就支持异步callback
```

## 动态编程，反射和元数据编程，数据和程序之间的相互转化机制，运行时编译和执行的机制，有抱负的开发者在这块可以多下些功夫，能够使你对语言的认识高出一个层面；

```javascript
//javascript本来就是动态语言,根本不需要反射
```

## 如果有必要，可研究一下该语言对于泛型的支持，不必花太多时间，只要能使用现成的泛型集合和泛型函数就可以了，可在以后闲暇时抽时间系统学习。需要注意的是，泛型技术跟多线程技术一样，用不好就成为万恶之源，必须系统学习，谨慎使用，否则不如不学不用；

```javascript
//javascript本来就是动态语言, 因为没有类型
// 真正需要程序员注意的泛型，是TypeScript
```

## 如果还有时间，最好咨询一下有经验的人，看看这个语言较常用的特色features是什么，如果之前没学过，应当补一下。比如Ruby的block interator, Java的dynamic proxy，C# 3的LINQ和extension method。没时间的话，我认为也可以边做边学，没有大问题。

```javascript
//javascript本来就是动态语言, 因为没有类型
// 真正需要程序员注意的泛型，是TypeScript
```

## 有必要的话，在工作的闲暇时间，可以着重考察两个问题，第一，这个语言有哪些惯用法和模式，第二，这个语言的编译/解释执行机制。
