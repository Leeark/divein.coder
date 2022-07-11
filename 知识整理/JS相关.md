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