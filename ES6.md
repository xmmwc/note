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

以下结果我也不知道咋回事


```
"use strict";

let someObject = {
    name:'this is name',
    someFunc:function(){
        return this.name;
    },
    someArrowFunc:()=>{
        return this.name;
    },
    someCallBackFunc:function(callback){
        callback.bind(this)();
    }
};

console.log('name is %s',someObject.someFunc());
console.log('name is %s',someObject.someArrowFunc());

someObject.someCallBackFunc(function(){
    console.log('name is %s',this.name);
});

someObject.someCallBackFunc(()=>{
    console.log('name is %s',this.name);
});

//name is this is name
//name is undefined
//name is this is name
//name is undefined
```



> 箭头函数会自动绑定 this 为定义时所在的上下文 ，而不是执行时候的上下文。

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

留坑，没看完。。。