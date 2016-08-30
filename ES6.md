## let and const

> 函数级作用域

```
function test() {
  var hello = 'world';
  console.log(hello);
}
test(); // 'world'
console.log(hello); // Error: hello is not defined
```

> 块级作用域

```
if(true) {
  var hello = 'world';
  console.log(hello); // 'world'
}
console.log(hello); // 'world'
```

### var 命令

```
if(true) {
  var hello = 'world';
  console.log(hello); // 'world'
}
console.log(hello); // 'world'
```

### let 命令

```
if(true) {
  let hello = 'world';
  console.log(hello); // 'world'
}
console.log(hello); // Error: hello is not defined
```

### const 命令


使用 const 命令声明常量

```
const STATUS_NOT_FOUND = 404;
```

常量的值为只读，不能修改

```
STATUS_NOT_FOUND = 200;
// SyntaxError: "STATUS_NOT_FOUND" is read-only
```

## Template String

传统的字符串

```
var name = 'es6';

var sayhello = 'hello, \
my name is ' + name + '.';

console.log(sayhello); 
```

输出：

```
hello, my name is es6.
```

ES6 模板字符串

```
var name = 'es6';

var sayhello = `hello,
my name is ${name}.`;

console.log(sayhello);
```

输出：

```
hello,
my name is es6.
```

> 空格和换行都会被保留

## Arrow Function

允许使用 => 定义函数。

```
x => x+1
```

等同于匿名函数

```
function (x) {
  return x + 1;
}
```

### 作用域

> 这个箭头函数的作用域和其他函数有一些不同,如果不是严格模式，`this`关键字就是指向`window`，**严格模式**就是`undefined`，在构造函数里的`this`指向的是当前对象实例,如果`this`在一个对象的函数内则`this`指向的是这个对象


> 当我们使用箭头函数时，函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
并不是因为箭头函数内部有绑定`this`的机制，实际原因是箭头函数根本没有自己的`this`，它的`this`是继承外面的，因此内部的`this`就是外层代码块的`this`。


```
 var name = 'global';

var someObject = {
    name: 'name',
    someFunc: function () {
      return this.name;
    },
    someArrowFunc: ()=> {
      return this.name;
    }
};

var b = someObject.someFunc;
var c = someObject.someArrowFunc;
var d = someObject.someArrowFunc.bind(someObject);

//隐式绑定this
console.log('name is %s', someObject.someFunc());//name is name
console.log('name is %s', someObject.someArrowFunc());//name is global
console.log('name is %s', b());//name is global
console.log('name is %s', c());//name is global
//被硬绑定的箭头函数
console.log('name is %s', d());//name is global
```



> 箭头函数会自动绑定 `this` 为定义时所在的上下文 ，而不是执行时候的上下文。

```
function doSomething(){
    this.name = "Some Function";

    setTimeout(function(){
        console.log('name is %s',this.name);
    },0);

    setTimeout(()=>{
        console.log('name is %s',this.name);
    },0);
}

doSomething();

//name is undefined
//name is Some Function
```

## Promise

> 先mark在这，以后填坑


## Generator

```
function *gen() {
    yield 'hello';
    yield 'world';
    return true;
}

var iter = gen();
var a = iter.next();
console.log(a); // {value:'hello', done:false}
var b = iter.next();
console.log(b); // {value:'world', done:false}
var c = iter.next();
console.log(c); // {value:true, done:true}

```

## destructuring

ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

看下面的例子：

```
let cat = 'ken'
let dog = 'lili'
let zoo = {cat: cat, dog: dog}
console.log(zoo)  //Object {cat: "ken", dog: "lili"}
```

用ES6完全可以像下面这么写：

```
let cat = 'ken'
let dog = 'lili'
let zoo = {cat, dog}
console.log(zoo)  //Object {cat: "ken", dog: "lili"}
```

反过来可以这么写：

```
let dog = {type: 'animal', many: 2}
let { type, many} = dog
console.log(type, many)   //animal 2
```

## import export

> 传统的写法

定义:

```
//content.js
define('content.js', function(){
    return 'A cat';
})
```

require:

```
//index.js
require(['./content.js'], function(animal){
    console.log(animal);   //A cat
})

```

CommonJS:

```
//index.js
var animal = require('./content.js')

//content.js
module.exports = 'A cat'

```

> ES6写法

```
//index.js
import animal from './content'

//content.js
export default 'A cat'
```

## ES6 module的其他高级用法

```
//content.js

export default 'A cat'    
export function say(){
    return 'Hello!'
}    
export const type = 'dog' 
```

```
//index.js

import { say, type } from './content'  
let says = say()
console.log(`The ${type} says ${says}`)  //The dog says Hello
```

> 这里输入的时候要注意：大括号里面的变量名，必须与被导入模块（content.js）对外接口的名称相同。

### 修改变量名

此时我们不喜欢type这个变量名，因为它有可能重名，所以我们需要修改一下它的变量名。在es6中可以用as实现一键换名。

```
//index.js

import animal, { say, type as animalType } from './content'  
let says = say()
console.log(`The ${animalType} says ${says} to ${animal}`)  
//The dog says Hello to A cat
```

### 模块的整体加载

除了指定加载某个输出值，还可以使用整体加载，即用星号（`*`）指定一个对象，所有输出值都加载在这个对象上面。

```
//index.js

import animal, * as content from './content'  
let says = content.say()
console.log(`The ${content.type} says ${says} to ${animal}`)  
//The dog says Hello to A cat
```

通常星号`*`结合`as`一起使用比较合适。

---

原处：

* [30分钟掌握ES6/ES2015核心内容（上）（下）](https://segmentfault.com/a/1190000004365693)
* [ES6 走马观花](https://segmentfault.com/a/1190000003764489)
