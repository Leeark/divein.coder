# 跨域问题

https://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html

什么是跨域？

一个url由协议、域名、端口 三部分组成。当一个请求url的`协议`、`域名`、`端口`三者之间的`任意一个`与当前页面url`不同`即为`跨域`。

原因：  浏览器遵循同源策略。

同源策略是一个重要的安全策略，它用于限制一个origin的文档或者它加载的脚本如何能与另一个源的资源进行交互。 它能帮助阻隔恶意文档，减少可能被攻击的媒介。

同源策略（Same Orgin Policy）是一种约定，它是浏览器核心也最基本的安全功能，它会阻止一个域的js脚本和另外一个域的内容进行交互，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。
所谓同源（即在同一个域）就是两个页面具有相同的协议（protocol）、主机（host）和端口号（port）。

解决：

1；后端配置响应头。

```js
header('Access-Control-Allow-Origin:*');//允许所有来源访问
header('Access-Control-Allow-Method:POST,GET');//允许访问的方式
```

2；jasonp请求

3；Nginx反向代理





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