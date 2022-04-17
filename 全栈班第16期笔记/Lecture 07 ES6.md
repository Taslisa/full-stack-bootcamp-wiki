# Lecture 07 ES6

## 主要知识点
- [Lecture 07](#lecture-07)
  - [主要知识点](#主要知识点)
- [课堂笔记](#课堂笔记)
  - [7.0 ES6](#70-es6)	 
  - [7.1 var vs let and const](#71-let-and-const)
  - [7.2 Template String](#72-template-string)
  - [7.3 Spread operator](#73-spread-operator)
  - [7.4 Destructuring](#74-destructuring)
  - [7.5 Default parameters](#75-default-parameters)
  - [7.6 Arrow function](#76-arrow-function)
  - [7.7 this](#77-this)
  - [7.8 Common array operations](#78-common-array-operations)
  - [7.9 Set](#79-set)
  - [7.10 Classes](#710-classes)
  - [7.11 Closure](#711-closure)
# 课堂笔记

### Lecture 07

#### 7.0 ES6
- ES(ECMAScript)
- ECMA指Ecma international 是一个指定javascript语法规则的机构，ES5在2009年发行，ES6在2015年发行，从2015年，机构决定每一年发布一个新的规范
- ES6代表了包括ES6及其以上的所有版本
- 浏览器只能理解ES5的语法，因此需要用Babel进行代码转译
#### 7.1 var vs let and const

They all used for variable declaration, the main difference is the scope.
- 用来申明变量，但是作用域不同
- 三种作用域：glocal scope，function scope，block scope块级作用域
### var
#### Scope

var is function scoped, it means if the variable is declared within a function, it can be accessed within the function. Similarly, if var is used outside of the function, the variable can be accessed in via window object. (in the browser)
- 变量放在function外面，function取得到其的值

```js
var apple = 'apple';
function foo() {
  var pear = 'pear';
  console.log(apple); // apple
  console.log(pear); // pear
}
console.log(apple); // apple
console.log(pear); // Uncaught ReferenceError: pear is not defined
```

#### Re-declare and update
- 用var的时候，重新申明和更新都是允许的
```js
var fruit = 'apple';
var fruit = 'pear';
console.log(fruit); // pear
fruit = 'grape';
console.log(fruit); // grape
```

#### Hoisting
- 把‘fruit’变量提升到了最上面，但只是提升了变量的声明，没有提升变量的赋值
```js
console.log(fruit); // undefined
var fruit = 'apple';
```

equals

```js
var fruit;
console.log(fruit); // undefined
fruit = 'apple';
```
- var fruit 不会报错，但实际写的时候不会用这样的写法
#### Problem
- 如果在函数里有一个变量，它是提升到当前函数的最上面，而不是当前文件的最上面
- 在开发中，如果导入的不同javascript文件中有名字重复的变量，会导致后一个变量的赋值将前一个改写，解决的方法一般用let或者模块化处理
```js
var fruit = 'apple';
if (true) {
  // think about this is in another file
  var fruit = 'pear';
}//because it is not a function,var's value can be changed
console.log(fruit); // pear
```
- 在实际写代码中，最好把所有的变量声明在最上面，方便检查
### let
- let可以完美替换 var 的使用
#### Scope
- let is block scoped. A block is a chunk of code wrapped by currly brackets `{}`
for example:
- block作用域指被括号{}括起来的部分
`function() {// this is a block}`
`if(true) {// this is also a block}`
let's reuse the example above but replace the keyword with _let_

```js
let fruit = 'apple';
if (true) {
  let fruit = 'pear';
}
console.log(fruit); // apple
```

#### Re-declare and update
不能用let重新申明但可以用let更新
```js
let fruit = 'apple';
// let fruit = "pear"; // Uncaught SyntaxError: Identifier 'fruit' has already been declared
fruit = 'grape';
console.log(fruit); // grape
```

#### Hoisting

```js
console.log(fruit); // Uncaught ReferenceError: Cannot access 'fruit' before initialization
let fruit = 'apple';
```i
- 在实际写代码中我们都事先声明变量再写，因此我们不会碰到这个问题
Different to _var_, let is hoisted, but the variable is not initialized
- 在nested loop，每个let的作用域就是包着它的那个{}块的范围
### const

Scope and the hoisting is the same as _let_

#### Re-declare
使用const指代primitive value时，不能对其值做更新
```js
const fruit = 'apple';
// const fruit = "pear"; // Uncaught SyntaxError: Identifier 'fruit' has already been declared
fruit = 'grape'; // Uncaught TypeError: Assignment to constant variable.
console.log(fruit);
```

#### Update

```js
const fruit = { name: 'apple', color: 'red' };
// fruit = {name: "apple", color: "green"}; // Uncaught TypeError: Assignment to constant variable.
fruit.color = 'green';
console.log(fruit); // {name: "apple", color: "green"}
```

similar in array

```js
const fruits = [];
// fruits = ["apple"]; // Error
fruits.push('apple');
console.log(fruits); // ["apple"]
```
- 在对array、object类型进行赋值时，改变的是地址里储存的值，指代fruit的地址没有改变，所以不会出错
>在实际开发中，能写‘let’就写‘let’，如果要写的variable是array或者object，可以换成‘const’

### Others

```js
console.log(fruit); // Uncaught ReferenceError: fruit is not defined
```

### Quiz

1. What's the output of the following code

```js
var i = 5;
for (var i = 0; i < 3; i++) {
  console.log(i); //012，i的值会一直increment，只有increment到超过这个终止条件后才能够跳出，也就是说只有i为4的时候才会跳出
}
console.log(i);//3
```

2. What's the output of the following code

```js
let i = 5;
for (let i = 0; i < 3; i++) {
  console.log(i);  // 012
}
console.log(i);// 5
```

3.

```js
var arr = [10, 12, 15, 21];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function () { //setTimeout是异步函数，当执行到异步函数时，会跳过这个函数，只有当异步函数的条件被触发时，才会回过来执行
    console.log('Index: ' + i + ', element: ' + arr[i]);
  }, 1000);
}
// Index: 4, element: undefined
// Index: 4, element: undefined
// Index: 4, element: undefined
// Index: 4, element: undefined
```
```js
function expression:
const foo = function(){};

function declaration:
function foo(){};
```

### Conclusion

| keyword | scope    | re-declare | update | hoisting              |
| ------- | -------- | ---------- | ------ | --------------------- |
| var     | function | Yes        | Yes    | Yes (undefined)       |
| let     | block    | No         | Yes    | Yes (not initialized) |
| const   | block    | No         | No     | Yes (not initialized) |

Extra reading source
[Var, Let, and Const – What's the Difference?](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)

## Template String

Also named, template literal, string interpolation

```js
const name = 'mason';
const age = 104;
// es5
console.log('My name is ' + name + ", and I'm " + age + ' years old');

//es6
console.log(`My name is ${name}, and I\'m ${age} years old`);
```

## Spread operator
- 克隆array以及object，或者把原本的元素原原本本地复制下来，在前后添加新的元素
```js
const array = [1, 2];
const newArray = [...array, 3, 4];
console.log(newArray); // [1, 2, 3, 4]
```

```js
const fruit = { name: 'apple', color: 'green' };
let newFruit = { ...fruit, color: 'red' };
console.log(newFruit); // {name: "apple", color: "red"}
newFruit = { color: 'red', ...fruit };
console.log(newFruit); // {color: "green", name: "apple"}
```
shallow/deep clone
```js
const fruit = {name: 'apple', price: 12, color: 'green', location: {city: 'brisbane'}};
const newFruit = {...fruit};//浅拷贝能clone的只有一层
//问题：因为shallow clone浅拷贝clone的是object{city: 'brisbane'}的reference，所以如果改变newFruit的object属性，原object也会改变
newFruit.location.city = 'sydney';
fruit.location.city => sydney;

*** newFruit = Fruit //相当于用一个新的指代newFruit指向了Fruit的地址，没有copy发生
```
[deep clone](https://flaviocopes.com/how-to-clone-javascript-object/)

## Destructuring
- 解构赋值
Object destructuring extracts property from object and assigns it to variables.
One way would be using the dot notation

```js
const fruit = { name: 'apple', color: 'red' };
const name = fruit.name; // apple
const color = fruit.color; // red
```

With the new syntax, we don't need to repeatly refer to the `fruit` object

```js
const fruit = { name: 'apple', color: 'red' };
const { name, color } = fruit;
console.log(name); // apple
console.log(color); // red
```

we can also rename the variable

```js
const fruit = { name: 'apple', color: 'red' };
const { name: fruitName, color: fruitColor } = fruit;
console.log(fruitName); // apple
console.log(fruitColor); // red
```
> 获取object的key value：object.keys()

or desctructing an array
- 解构array要注意数据的有序性
```js
const fruits = [
  { name: 'apple', color: 'red' },
  { name: 'pear', color: 'green' },
];
//注意左边的结构要与右边一致，fruit是'[]',左边也要写成'[]'
const [apple, pear] = fruits;
console.log(apple); // {name: "apple", color: "red"}
console.log(pear); // {name: "pear", color: "green"}
const [{ color: appleColor }, { color: pearColor }] = fruits;
console.log(appleColor); // red
console.log(pearColor); // green


const [{ name: appleName，color}, { name: pearName }] = fruits;
console.log(appleName); // apple
console.log(pearName); // pear
console.log(color); // red
```

more complicated use cases

```js
const [foo, [[bar], baz]] = [1, [[2], 3]];
console.log(foo); // 1
console.log(bar); // 2
console.log(baz); // 3
```

```js
const [, , third] = ['foo', 'bar', 'baz'];
console.log(third); // "baz"
```

```js
const [head, ...tail] = [1, 2, 3, 4];
console.log(head); // 1
console.log(tail); // [2, 3, 4]
// Rest element must be last element
```

```js
const [missing = true] = [];
console.log(missing); // true
```

## Default parameters

```js
function sum(a = 1, b = 1) {
  return a + b;
}
console.log(sum()); // 2
console.log(sum(undefined, 2)); // 3
console.log(sum(3, 4)); // 7
```

## Arrow function

```js
const add = function (x, y) {
  return x + y;
};
// vs
const add = (x, y) => {
  return x + y;
};
当整个body只有一行的时候：可简写成如下：
// equals
const add = (x, y) => x + y;
//返回object的情况
const add =(x,y) => ({sum:x+y});
```

### Callback

Explain in a simple way, pass the function as a parameter and when some _event_ happened (addEventListener), execute this function.
Frequently used for async or sequential purpose

```js
function logger(param) {
  console.log(param);
}
function sum(x, y, callback) {
  setTimeout(function () {
    const total = x + y;
    callback(total);
  }, 1000);
}
sum(1, 2, logger);
```
- callbackfunction解决的问题：如果把logger function写在sum function里面，每次执行sum必定会连着执行logger
### Callback with arrow function

```js
setTimeout(function () {
  console.log('normal function');
}, 1000);

setTimeout(() => {
  console.log('arrow function');
}, 1000);
```

## Closure

Closures are everywhere in JS. A closure is when a function has access to its lexical scope even when it is called outside of it. Closures are created every time a function is created, at function creation time.
- 我们想要访问一个变量，但是它在当前的作用域里不存在，我们需要查找他的上级作用域来看这个变量是否存在，当出现这种跨域操作的时候，称为闭包

A few complex but common closure cases:

1. a function was passed to another function as param

```js
// we normally don't write this code
const number = 1;
function foo() {
  console.log(number);//注意在严格模式下不能这么写
}
function bar(fn) {
  const number = 2;
  fn();
}
bar(foo); // 1
//Q：bar(foo)的结果为何不为2？const number = 2不是处于fn（）的上级作用域吗？
//A：因为闭包在函数书写下来的时候就已经形成了，foo（）函数在被创造时，上级作用域为const number = 1，这个区域又被称为lexical scope词法作用域
```


2. a function was returned by another function

```js
function foo() {
  const number = 1;
  return () => {
    console.log(number);
  };
}
const number = 100;//和调用函数上方写的值没有关系
foo()(); // 1
//foo()指返回一个函数，foo()()指执行这个返回的函数
```

We can use this technique to hide some data.

```js
function createCounter() {
  let counter = 0;
  const increment = () => {
    counter++;
  };
  const getCount = () => {
    return counter;
  };
  return {
    increment,
    getCount,
  };
}
const counter = createCounter();//无法直接对counter进行修改，只能使用暴露出来的函数increment()和getCount()
counter.increment();
console.log(counter.getCount());
```

### IIFEs

Immediately Invoked Function Expressions
Commonly used to avoid polluting the global namespace and modules!

```js
(function () {
  // some variable in it's own scope
})();
```

## this

In most cases, the value of `this` is determined by how a function is called (runtime binding). It can't be set by assignment during execution, and it may be different each time the function is called. [[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)]\* \*[strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) is enabled by default in ES6 modules
- this的目的是让我们理解context，在代码运行的时候谁在调用它，this就指向谁
### _this_ keyword in normal functions

```js
function foo() {
  console.log(this);
}
foo(); // window
//foo被注册在window这个对象上，即我们可以用window.foo()调用，而在普通函数里，谁调用了这个函数，this就指向谁，所以this指向了window
```

### _this_ keyword in normal functions with bind, call, apply
- 可以人为指定this对象
```js
// a1,a2
foo.call({ number: 1 }); // {number: 1}
// [a1,a2]
foo.apply({ number: 2 }); // {number: 2}
// bind returns a new function
const bar = foo.bind({ number: 3 });
bar(); // {number:3}
```

### _this_ keyword in an object and callback functions

```js
const calendar = {
  currentDay: 6,
  nextDay() {
    this.currentDay++;
    console.log(this.currentDay);
  },
};
calendar.nextDay();//7
```

```js
const calendar = {
  currentDay: 6,
  nextDay() {
    setTimeout(function () { //此处函数没有被调用，只是被传给了setTimeout
      this.currentDay++;
      console.log(this.currentDay);
    }); // .bind(this) <- 这个this指向calender，因此加上bind(this)可以输出 7
  },
};
calendar.nextDay(); //setTimeout这个函数的作用是，在数到多少秒后，让window调用在其中的function，因此这里的this指向window，因为windoe没有currentDay这个property，输出NaN（因为无法把一个undefined’currentDay‘和一个数字’1‘加在一起）
```

In arrow function, `this` points to the enclosing lexical context's `this`.

```js
const calendar = {
  currentDay: 6,
  nextDay() {
    setTimeout(() => { //它的上级作用域的this指向哪里，这个arrow function的this就指向哪里。此处它的上级作用域在nextDay()里面
      this.currentDay++; 
      console.log(this.currentDay);
    });
  },
};
calendar.nextDay();

nextDay(){}也可以拆成： //因此this的上级作用域为nextDay()
nextDay() {
    const cb = () => { 
      this.currentDay++; 
      console.log(this.currentDay);
    };
    setTimeout(cb);
}

```

```js
const calendar = {
  currentDay: 6,
  normal: function () {
    console.log(1, this); //calendar
    setTimeout(function () {
      console.log(2, this);//window
    });
  },
  arrow: function () {
    console.log(3, this); //calendar
    setTimeout(() => {
      console.log(4, this);//calender
    });
  },
};
calendar.normal();
calendar.arrow();

Answer：
1 {currentDay: 6, normal: ƒ, arrow: ƒ}
3 {currentDay: 6, normal: ƒ, arrow: ƒ}

2 Window {0: global, 1: global, 2: global, 3: global, 4: Window, 5: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
4 {currentDay: 6, normal: ƒ, arrow: ƒ}
//先输出3后输出2是因为3是同步代码，2是异步代码，必须等到call stack里的所有任务清空后才会执行在宿舍                                                                                                                                                                                                                                                                                                                                                  

```

### quiz

```js
const object = {
  message: 'Hello, World!',

  getMessage() {
    const message = 'Hello, Earth!';
    return this.message;
  },
};

console.log(object.getMessage()); //  'Hello, World!'
```

```js
const object = {
  who: 'World',

  greet() {
    return `Hello, ${this.who}!`;
  },

  farewell: () => {
    return `Goodbye, ${this.who}!`;
  },
};

console.log(object.greet()); // Hello World
console.log(object.farewell()); // Goodbye undefined 因为farewell作为箭头函数，其中的this指向的是上级作用域，而object的{}不算是一个block scope，因此object里的this指向的是window，farewell()里的this指向的是window

const obj ={
	greet() {
	
	},
	greets:function(){
	
	},
	greet2:()=>{}
}
//object literal
const obj = {};
obj.greet = function(){}
obj.greet1 = function(){};
obj.greet2 = () => {}
```

```js
const object = {
  who: 'mason',
  cb() {
    console.log(`Hello, ${this.who}!`);
  },
};

function foo(cb) {
  cb();
}
//equals
function foo(cb) {
  console.log(`Hello, ${this.who}!`);//this指向window
}

foo(object.cb); // Hello undefined
object.cb(); // Hello mason
```

## Common array operations

### Manipulation

```js
const fruits = ['apple'];

fruits.push('pear');//push 尾部添加
console.log(fruits); // ["apple", "pear"]
fruits.unshift('grape');//unshift 头部删除
console.log(fruits); // ["grape", "apple", "pear"]
// splice(x,y,newAdded)
// remove y items from index x, and add newAdded
fruits.splice(1, 1, 'watermelon', 'peach');
console.log(fruits); // ["grape", "watermelon", "peach", "pear"]
let fruit = fruits.pop();
console.log(fruit); // pear
console.log(fruits); //  ["grape", "watermelon", "peach"]
fruit = fruits.shift();
console.log(fruit); // grape
console.log(fruits); // ["watermelon", "peach"]
```

### Iteration

#### for loop

```js
const fruits = ['apple', 'pear'];
for (let index = 0; index < fruits.length; index++) {
  const fruit = fruits[index];
  console.log(fruit);
}
// apple
// pear
```

#### for...of

```js
const fruits = ['apple', 'pear'];
for (let fruit of fruits) {
  console.log(fruit);
}
// apple
// pear

// for...in -> 0, 1    usually used in object
```

#### forEach

```js
const fruits = ['apple', 'pear'];
fruits.forEach((fruit) => console.log(fruit));
// apple
// pear
// cannot use break here forEach一定会把每一项都取出来遍历一遍
```

### Map
- 映射，在保证原始数组和新数组长度一致的情况下，用于把原始数组映射到新数组
```js
const fruits = ['apple', 'pear'];
const newFruits = fruits.map((fruit) => ({
  name: fruit,
  price: 10,
}));
console.log(newFruits);
// [{name: "apple", price: 10},{name: "pear", price: 10}]
```

### Reduce

```js
const numbers = [1, 2, 3];
const sum = numbers.reduce((accumulator, number) => accumulator + number, 0);
console.log(sum); // 6
```

### Search

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.includes(2)); // true
// Array.some
console.log(numbers.indexOf(2)); // 1
// Array.findIndex
```

```js
const numbers = [1, 2, 3, 4, 5];
const odds = numbers.filter((i) => i % 2);//filter会把整个数组遍历一遍，找到所有符合要求的元素
console.log(odds); // [1,3,5]

const fruits = [
  {
    name: 'apple',
    color: 'red',
  },
  {
    name: 'pear',
    color: 'green',
  },
  {
    name: 'grape',
    color: 'green',
  },
];
const filteredFruits = fruits.filter((i) => i.color === 'green');
console.log(filteredFruits);
// [{name: "pear", color: "green"}, {name: "grape", color: "green"}]
```

```js
//在 ES5 中，要在数组中查找元素，可以使用 indexOf() 或 lastIndexOf() 方法。但是，这些方法非常有限，因为它们只返回第一个匹配元素的索引。

//ES6 引入了一个名为 find() 的新方法，添加到 Array.prototype 对象中。
//find会返回第一个匹配元素的元素本省
const fruits = [
  {
    name: 'apple',
    color: 'red',
  },
  {
    name: 'pear',
    color: 'green',
  },
  {
    name: 'grape',
    color: 'green',
  },
];
const greenFruit = fruits.find((i) => i.color === 'green');//查看返回的值是否为True
console.log(greenFruit);
// {name: "pear", color: "green"}
```

#### Extra reading source

[link](https://dmitripavlutin.com/operations-on-arrays-javascript/)

## Set

Set is a data structure, we use it to store _unique_ values.

```js
const set = new Set([1, 2, 3, 4, 4]);
console.log(set); // Set(4) {1, 2, 3, 4}
set.add(5);
console.log(set); // Set(5) {1, 2, 3, 4, 5}
set.add(1);
console.log(set); // Set(5) {1, 2, 3, 4, 5}
console.log(set.has(5)); // true
set.delete(1);
console.log(set.has(1)); // false
console.log(set.size); // 4
```

```js
//对array进行去重
const array = [1, 2, 2, 3, 4, 4];
const uniqueArray = [...new Set(array)];
console.log(uniqueArray); // [1, 2, 3, 4]
//注意如果array中有object，且写的形式如下
const set = new Set()
const a = {a:1}
const b = {a:1}
// Set 不会对[a,b]去重，因为两个object的reference不一样
//注意object里不能出现重复的属性，如果出现的话，后面的value会把前面的覆盖掉
```

## Classes
- ES6新引入的属性，可以把其代码写成类似java里的class，但其本质还是function
- 在javascript里，inheritance继承是基于原型Prototype
Classes are a template for creating objects. Classes are in fact functions, class is only a syntax sugar（语法糖).

```js
function Person(name) {
  this.name = name;
  this.toString = function () {
    console.log('name: ' + this.name);
  };
}
var mason = new Person('mason');
mason.toString(); // name: mason

//if coded like this:
var mason = Person('mason');//就是调用一个普通函数
object === undefined // True 原函数没有声明return的话，默认return:undefined；
```

```js
//换了一个名字的function，但是class会自动绑定相应的原型，不再需要bind()
class Person {
  constructor(name) {
    this.name = name;
  }
  toString() {
    console.log(`name: ${this.name}`);
  }
}
const mason = new Person('mason');
mason.toString(); // name: mason
```

### extends

```js
class Teacher extends Person {
  constructor(name) {
    super(name);
  }
  teach() {
    console.log(`${this.name} is teaching`);
  }
}

const mason = new Teacher('mason');
mason.teach(); // mason is teaching
mason.toString(); // name: mason -> BUT how?
//子类继承父类后，可以使用父类的constructor()和methods

//if code like this:
function Person(name) {
  this.name = name;
  this.toString = function () {
    console.log('name: ' + this.name);
  };
  return 1;
}
const mason = new Person("")
mason // Person{name:'',toString:f} 会把原本的return:1；覆盖掉

//if code like this：
function Person(name) {
  this.name = name;
  this.toString = function () {
    console.log('name: ' + this.name);
  };
  return {a:1};
}
const mason = new Person("")
mason //{a：1} 不会被替换掉
```

```js
// is mason constructed by Teacher?
mason instanceof Teacher; // true
mason instanceof Person; // true
mason instanceof Object; // true
```

## quiz

```js
function Pet(name) {
  this.name = name;
  this.getName = () => this.name;
}

const cat = new Pet('Fluffy');

console.log(cat.getName()); // Fluffy

const { getName } = cat;
console.log(getName()); // Fluffy
```

```js
var scope = 'global scope';
function checkscope() {
  var scope = 'local scope';
  function f() {
    return scope;
  }
  return f();//返回function执行的结果
}
checkscope(); // local
```

```js
var scope = 'global scope';
function checkscope() {
  var scope = 'local scope';
  function f() {
    return scope;
  }
  return f;
}
checkscope()(); // local
```

Quiz questions references
[1](https://dmitripavlutin.com/javascript-this-interview-questions/#question-1-variable-vs-property)