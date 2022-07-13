

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