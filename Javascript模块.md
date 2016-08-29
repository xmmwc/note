### 模块模式

```
var someFn = function () {
    var i = 'someString';
    var j = {
        text: 'i am some Object'
    };

    var printSomeString = function () {
        console.log(i);
    };

    var getSomeString = function () {
        return i;
    };

    var getSomeObject = function () {
        return j;
    };

    return {
        printSomeString: printSomeString,
        getSomeString: getSomeString,
        getSomeObject: getSomeObject
    }
};

var a = someFn();
var b = someFn();
var c = new someFn();

console.log(a === b);//false
console.log(a === c);//false

console.log(a.getSomeString() === b.getSomeString());//true
console.log(a.getSomeString() === c.getSomeString());//true

console.log(a.getSomeObject() === b.getSomeObject());//false
console.log(a.getSomeObject() === c.getSomeObject());//false
```

> “代码中有一个叫作`someFn()`的独立的模块创建器，可以被调用任意多次，每次调用都会创建一个新的模块实例。”

摘录来自: Kyle Simpson、赵望野、梁杰. “你不知道的JavaScript（上卷）” [有改动]。 

> 如果构造函数中返回了一个对象，那么new出来的对象将会被返回的对象覆盖。模块模式的结果是`a`和`b`都从返回的对象copy了一份属性和方法，它们之间互不影响。继承关系也变了，`a`和`b`都直接继承于Object

** 问：这里面的`someFn()`和`new someFn()`有啥区别？ **


Module模式的还是存在一定的不足：
 
1. 由于我们访问公有和私有成员的方式不同，当我们想改变可见性时，实际上我们必须修改每一个曾经使用过该成员的存在。 
2. 我们无法访问那些之后在方法里面添加的私有成员， 
3. 无法为私有成员创建自动化单元测试，bug需要修正补丁时会增加额外的复杂性。 
4. 开发人员无法轻易地扩展私有方法




### 对象字面量

```
var oneModule = {
    var1: 1,
    var2: 'a',
    method1: function () {
        return this.var1;
    },
    method2: function () {
        return this.var1 + this.var2;
    }
};
```

不足：没办法有私有成员

### 构造函数方式

```
var twoModule = function () {
    this.name = 'two';
    this.method = function () {
        return this.name;
    }
};
```

### prototype原型方式

```
var twoModule = function () {
    this.name = 'two';
    this.method = function () {
        return this.name;
    };
    this.method1 = function (name) {
        return name;
    };
};

twoModule.prototype.method1 = function () {
    return this.method(this.name);
};
```


> 值得注意的是`method`和`method1`都属于twoModule的方法
而`method1`也属于`twoModule`的`prototype`上的方法，但是`twoModule.prototype.method1.prototype`指向的是`twoModule.method1`
