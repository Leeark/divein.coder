

# JS数据类型

ECMAScript有6种简单数据类型（也称为原始类型）: Undefined、Null、Boolean、Number、String和Symbol。

Symbol（符号）是ECMAScript 6新增的。

还有一种复杂数据类型叫Object（对象）。

# JS判断数据类型：

https://www.cnblogs.com/onepixel/p/5126046.html

## typeof操作符

对一个值使用typeof操作符会返回下列字符串之一：

❑ "string"表示值为字符串；❑ "number"表示值为数值；❑ "symbol"表示值为符号。

❑ "object"表示值为对象（而不是函数）或null；❑ "function"表示值为函数；

❑ "undefined"表示值未定义；❑ "boolean"表示值为布尔值；

缺点：

1,typeof null ; //'object'

2,无法区分对象（除了函数）的具体类型

3,new Boolean()；new Number()；new String()检测为'object'![image-20220714104045998](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220714104045998.png)

## instanceof

instanceof 是用来判断 A 是否为 B 的实例，表达式为：A instanceof B，如果 A 是 B 的实例，则返回 true,否则返回 false。 （检测构造函数的prototype是否出现在某个实例对象的原型链上）

new出的实例同时是两个构造函数的实例![image-20220714104241794](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220714104241794.png)

```js
[] instanceof Array; // true
{} instanceof Object;// true
new Date() instanceof Date;// true
 
function Person(){};
new Person() instanceof Person;// true
 
[] instanceof Object; // true
new Date() instanceof Object;// true
new Person instanceof Object;// true
```

因此，**instanceof 只能用来判断两个对象是否属于实例关系****， 而不能判断一个对象实例具体属于哪种类型。**

## constructor

当一个函数 F被定义时，JS引擎会为F添加 prototype 原型，然后再在 prototype上添加一个 constructor 属性，并让其指向 F 的引用。如下所示：

![img](https://images2015.cnblogs.com/blog/849589/201705/849589-20170508125250566-1896556617.png)

当执行 var f = new F() 时，F 被当成了构造函数，f 是F的实例对象，此时 F 原型上的 constructor 通过原型链传递到了 f 上，因此 f.constructor == F

![img](https://images2015.cnblogs.com/blog/849589/201705/849589-20170508125714941-1649387639.png)

## toString

toString() 是 Object 的原型方法。可以通过 `toString()` 来获取每个对象的类型。为了每个对象都能通过 `Object.prototype.toString()` 来检测，需要以 `Function.prototype.call()` 或者 `Function.prototype.apply()` 的形式来调用，传递要检查的对象作为第一个参数，称为 `thisArg`。

对于 Object 对象，直接调用 toString() 就能返回' [object Object] '。而对于其他对象，则需要通过 call / apply 来调用才能返回正确的类型信息。

```js
Object.prototype.toString.call('') ;   // [object String]
Object.prototype.toString.call(1) ;    // [object Number]
Object.prototype.toString.call(true) ; // [object Boolean]
Object.prototype.toString.call(Symbol()); //[object Symbol]
Object.prototype.toString.call(undefined) ; // [object Undefined]
Object.prototype.toString.call(null) ; // [object Null]
Object.prototype.toString.call(new Function()) ; // [object Function]
Object.prototype.toString.call(new Date()) ; // [object Date]
Object.prototype.toString.call([]) ; // [object Array]
Object.prototype.toString.call(new RegExp()) ; // [object RegExp]
Object.prototype.toString.call(new Error()) ; // [object Error]
Object.prototype.toString.call(document) ; // [object HTMLDocument]
Object.prototype.toString.call(window) ; //[object global] window 是全局对象 global 的引用
```

# Object 构造函数的方法

## Object.create()

**`Object.create()`** 方法用于创建一个新对象，使用现有的对象来作为新创建对象的原型（prototype）。

```js
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // inherited properties can be overwritten

me.printIntroduction();
// expected output: "My name is Matthew. Am I human? true"
```

## Object.keys()

ES5 引入了`Object.keys`方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

## Object.values()

ES2017引入，`Object.values`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

## Object.entries()

ES2017引入，`Object.entries`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

## Object.is(a,b) 

它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

不同之处只有两个：一是 +0 不等于 -0 ，二是 NaN 等于自身。

## Object.assign() 

合并对象：将源对象（source）的所有**可枚举属性**，复制到目标对象（target）。

Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。

**注意**：如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```js
const target = { a: 1, b: 1 };
const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
console.log(target);    // {a:1, b:2, c:3}
```

## Object.freeze()

**`Object.freeze()`** 方法可以**冻结**一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改。`freeze()` 返回和传入的参数相同的对象。

## Object.defineProperty()

`Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。语法：

```reasonml
Object.defineProperty(obj, prop, descriptor)
```

参数说明：

> obj：必需。目标对象
> prop：必需。需定义或修改的属性的名字
> descriptor：必需。目标属性所拥有的特性

返回值：

> 传入函数的对象。即第一个参数obj

给对象的属性添加特性描述，目前提供两种形式：数据描述和存取器描述。

### 数据描述

value: 设置属性的值
writable: 值是否可以重写。true | false
enumerable: 目标属性是否可以被枚举。true | false
configurable: 目标属性是否可以被删除或是否可以再次修改特性（数据描述） true | false

```js
var obj = {
    test:"hello"
}
//对象已有的属性添加特性描述
Object.defineProperty(obj,"test",{
    configurable:true | false,
    enumerable:true | false,
    value:任意类型的值,
    writable:true | false
});
//对象新添加的属性的特性描述
Object.defineProperty(obj,"newKey",{
    configurable:true | false,
    enumerable:true | false,
    value:任意类型的值,
    writable:true | false
});
```



### 存取器描述

**getter/setter**

当设置或获取对象的某个属性的值的时候，可以提供getter/setter方法。

- getter 是一种获得属性值的方法
- setter是一种设置属性值的方法。

**注意：当使用了getter或setter方法，不允许使用writable和value这两个属性**

## Object.defineProperties()

该方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。

```js
var obj = {};
Object.defineProperties(obj, {
  'property1': {
    value: true,
    writable: true
  },
  'property2': {
    value: 'Hello',
    writable: false
  }
  // etc. etc.
});
```

## Object.setPrototypeOf() 

`Object.setPrototypeOf`方法的作用与`__proto__`相同，用来设置一个对象的原型对象（prototype），返回参数对象本身。它是 ES6 正式推荐的设置原型对象的方法。

```javascript
// 格式
Object.setPrototypeOf(object, prototype)

// 用法
const o = Object.setPrototypeOf({}, null);
```

该方法等同于下面的函数。

```javascript
function setPrototypeOf(obj, proto) {
  obj.__proto__ = proto;
  return obj;
}
```



## Object.getPrototypeOf()

该方法与`Object.setPrototypeOf`方法配套，用于读取一个对象的原型对象。

## Object.getOwnPropertyDescriptor()

**`Object.getOwnPropertyDescriptor()`** 方法返回指定对象上一个自有属性对应的属性描述符。（自有属性指的是直接赋予该对象的属性，不需要从原型链上进行查找的属性）

```js
const object1 = {
  property1: 42
};

const descriptor1 = Object.getOwnPropertyDescriptor(object1, 'property1');

console.log(descriptor1.configurable);
// expected output: true

console.log(descriptor1.value);
// expected output: 42
```



## Object.getOwnPropertyDescriptors()

ES5 的`Object.getOwnPropertyDescriptor()`方法会返回某个对象属性的描述对象（descriptor）。

ES2017 引入了`Object.getOwnPropertyDescriptors()`方法，返回指定对象所有自身属性（非继承属性）的描述对象。

```javascript
const obj = {
  foo: 123,
  get bar() { return 'abc' }
};

Object.getOwnPropertyDescriptors(obj)
// { foo:
//    { value: 123,
//      writable: true,
//      enumerable: true,
//      configurable: true },
//   bar:
//    { get: [Function: get bar],
//      set: undefined,
//      enumerable: true,
//      configurable: true } }
```

上面代码中，`Object.getOwnPropertyDescriptors()`方法返回一个对象，所有原对象的属性名都是该对象的属性名，对应的属性值就是该属性的描述对象。

## Object.getOwnPropertyNames()

**`Object.getOwnPropertyNames()`**方法返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括 Symbol 值作为名称的属性）组成的数组。

```js
Object.getOwnPropertyNames(obj)
```

## Object.getOwnPropertySymbols()

`Object.getOwnPropertySymbols()` 方法返回一个给定对象自身的所有 Symbol 属性的数组。

```js
Object.getOwnPropertySymbols(obj)
```

# 操作dom

## 获取

最常用的方法是`document.getElementById()`和`document.getElementsByTagName()`，以及CSS选择器`document.getElementsByClassName()`。

由于ID在HTML文档中是唯一的，所以`document.getElementById()`可以直接定位唯一的一个DOM节点。`document.getElementsByTagName()`和`document.getElementsByClassName()`总是返回一组DOM节点。

要精确地选择DOM，可以先定位父节点，再从父节点开始选择，以缩小范围。

第二种方法是使用`querySelector()`和`querySelectorAll()`，需要了解selector语法，然后使用条件来获取节点，更加方便：

Document.querySelector：方法返回文档中与指定选择器或选择器组匹配的第一个 [`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)对象。 如果找不到匹配项，则返回`null`。

Document.querySelectorAll：返回与指定的选择器组匹配的文档中的元素列表 (使用深度优先的先序遍历文档的节点)。返回的对象是 [`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList) 。

## 添加

移动DOM节点也就是把这个节点插入到html文档中的某个地方，这里js给了我们两个方法：

1.appendChild()：把节点插入到父节点的末尾。

document.body.appendChild(oDiv);  //把div插入到body中，并且位于末尾

2.insertBefore()：把节点插入到父节点的某个兄弟节点的前面。

var oP = createElement('p'); //创建一个p节点
document.body.insertBefore(oP,oDiv); //把p节点插入到div的前面

## 删除

删除DOM节点的方法是removeChild()。

document.body.removeChild(oP); //删除p节点

## 替换

替换DOM节点的方法是replaceChild()。

var oSpan = document.createElement('span'); //创建一个span标签
document.body.replaceChild(oSpan,oBox); //用span标签替换div标签

![image-20220713105004111](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220713105004111.png)

# 文档插入100节点，解决办法

解决办法：创建文档片段Fragment，将标签全部放入该片段中，再统一插入document，这样只会渲染一次

```javascript
<ul id="root"></ul>
<script>
var root = document.getElementById('root')
var fragment = document.createDocumentFragment()
for(let i = 0; i < 1000; i++){
	let li = document.createElement('li')
	li.innerHTML = '我是li标签'
    fragment.appendChild(li)
}
root.appendChild(fragment);
</script>
我们经常使用javascript来操作DOM元素，比如使用appendChild()方法。
每次调用该方法时，浏览器都会重新渲染页面。如果大量的更新DOM节点，则会非常消耗性能，影响用户体验.
javascript提供了一个文档碎片DocumentFragment的机制。
如果将文档中的节点添加到文档片段中，就会从文档树中移除该节点。
 
把所有要构造的节点都放在文档片段中执行，这样可以不影响文档树，也就不会造成页面渲染。
当节点都构造完成后，再将文档片段对象添加到页面中，这时所有的节点都会一次性渲染出来，
这样就能减少浏览器负担，提高页面渲染速度
```

# 作用域与作用域链

- 作用域分为全局作用域和局部作用域。
- 作用域其实就是规定了当前作用域中的变量和函数可被作用的范围。
- 作用域链其实就是规定了变量和函数的查找规则、是当前执行上下文的变量对象以及所有父级执行上下文的变量对象的集合。
- 当查找一个变量时，先从作用域的顶端查找，一直查找到作用域的底端，若查找完仍未找到，抛出错误。
- （块级作用域）
- var 声明是全局作用域或函数作用域，而 let 和 const 是块作用域。 var 变量可以在其范围内更新和重新声明； let 变量可以被更新但不能重新声明； const 变量既不能更新也不能重新声明。 它们都被提升到其作用域的顶端。

# 原型与原型链



# 数组方法





# 扩展运算符

# 解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

# 箭头函数



# promise

# 



# this指向

`this`指的是函数运行时所在的环境（上下文）。

1；浏览器：全局上下文中this指向window

2；普通函数：谁调用指向谁

全局函数：指向window； 对象调用方法：指向该对象。

3；箭头函数：外部指向谁就指向谁；在哪里定义就指向谁；没有自己的this；

4；构造函数中的this，指向新建出的实例对象。

new调用构造函数的过程：
1，创建新的临时对象a
2，把a的原型属性(<u>__</u>proto<u>__</u>)指向该构造函数原型属性(prototype)
3，把this绑定到a上
4，如果构造函数没返回其他对象，则返回a

5；dom事件中的this指向dom标签



# [Vue组件通信方法](D:\我爱学习\我爱前端\我爱面试\知识点总结\知识整理\Vue中的组件通信.md)







# 模块化

我们现在有了运行大量 JavaScript 脚本的复杂程序，还有一些被用在其他环境（例如 [Node.js](https://developer.mozilla.org/en-US/docs/Glossary/Node.js)）。因此，近年来，有必要开始考虑提供一种将 JavaScript 程序拆分为可按需导入的单独模块的机制。

# 防抖与节流

## 防抖

1.事件触发n秒后执行回调（延迟执行）2.n秒内再次触发事件，重新计时。

```js
// 实现 2
// immediate 表示第一次是否立即执行
function debounce(fn, wait = 50, immediate) {
    let timer = null
    return function(...args) {
        if (timer) clearTimeout(timer)
      
      	// ------ 新增部分 start ------ 
      	// immediate 为 true 表示第一次触发后执行
      	// timer 为空表示首次触发
        if (immediate && !timer) {
            fn.apply(this, args)
        }
      	// ------ 新增部分 end ------ 
      	
        timer = setTimeout(() => {
            fn.apply(this, args)
        }, wait)
    }
}

// DEMO
// 执行 debounce 函数返回新函数
const betterFn = debounce(() => console.log('fn 防抖执行了'), 1000, true)
// 第一次触发 scroll 执行一次 fn，后续只有在停止滑动 1 秒后才执行函数 fn
document.addEventListener('scroll', betterFn)
```

## 节流

限制一个函数在一定时间内只能执行一次。

```js
// fn 是需要执行的函数
// wait 是时间间隔
const throttle = (fn, wait = 50) => {
  // 上一次执行 fn 的时间
  let previous = 0
  // 将 throttle 处理结果当作函数返回
  return function(...args) {
    // 获取当前时间，转换成时间戳，单位毫秒
    let now = +new Date()
    // 将当前时间和上一次执行函数的时间进行对比
    // 大于等待时间就把 previous 设置为当前时间并执行函数 fn
    if (now - previous > wait) {
      previous = now
      fn.apply(this, args)
    }
  }
}

// DEMO
// 执行 throttle 函数返回新函数
const betterFn = throttle(() => console.log('fn 函数执行了'), 1000)
// 每 10 毫秒执行一次 betterFn 函数，但是只有时间差大于 1000 时才会执行 fn
setInterval(betterFn, 10)
```