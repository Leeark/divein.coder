<<<<<<< HEAD

# 1. Vue中的组件通信

## 1.1 父=====>子

step 1，父组件：为子组件标签绑定自定义属性，数据赋值：`:faMsg='msg'`。

step 2，子组件：添加props，写入自定义属性名:`props:['faMsg']`。

## 1.2 子=====>父

### 1.2.1 自定义属性实现

step 1，父组件：为子组件标签（在子组件的VC上）绑定自定义属性，属性值为一个回调函数`:FrSonMsg='getMsg'`。

step 2，子组件：添加props，接收函数:`props:['getMsg']`。

step 3，子组件：添加事件，函数中触发接收到的函数，传参。

### 1.2.2 自定义事件实现

#### 1.2.2.1 V-on或@写法

step 1，父组件：为子组件标签（在子组件的VC上）绑定自定义事件，以接收子组件数据，data里注册数据。

```vue
父组件：
<Template>
 <Son @numFromSon='getNum'/>
</Template>
    
<script>
import Son from "./components/Son";
    export default {
     name:'Father',
     data(){
       return {numFrSon:''}
     },
     methods:{
       getNum(val){
        this.numFrSon = val
       }
     }
    }
</script>
```

step 2，在子组件中用$emit触发自定义事件，数据以参数形式传递给父组件。

```vue
子组件：
<Template>
 <button @click='SendNum'><button/>
</Template>
    
<script>
    export default {
      name:'Son',
      data(){
       return {num:''}
      },
      methods:{
       SendNum(val){
        this.$emit('numFromSon',this.num)
       }
      }
     }
</script>
```

#### 1.2.2.2 ref写法（更灵活）

step 1，父组件：为子组件标签（在子组件的VC上）绑定ref，拿到子组件VC。

step 2，父组件：写入回调函数，接收数据。回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！

```js
<Demo ref="demo"/>
......
mounted(){
   this.$refs.demo.$on('atguigu',回调函数)
}
```

step 3，在子组件中用$emit触发自定义事件，数据以参数形式传递给父组件```this.$emit('atguigu',数据)```	。

## 1.3 兄弟（任意）组件通信：全局事件总线

### 两种方式：

#### 1.3.1 新建另一个Vue实例，向外共享。

step 1，新建eventBus.js，引入项目Vue，向外暴露新的Vue。

```js
// eventBus.js
import Vue from 'vue'
export const bus = new Vue()
```

step 2，需要通信的组件引入eventBus.js文件`import {bus} from './eventBus.js'`。

step 3，发送方自定义事件，调用`bus.$emit('事件名称'，发送的数据)`。

step 3，接收方在created钩子中，定义`bus.$on('事件名称'，(发送的数据)=>{this.msg = 发送的数据})`。

#### 1.3.2 在该Vue实例的原型上绑定$bus。

step 1，在main.js中添加以下代码，将`$bus`写入Vue实例的原型对象：

```js
new Vue({
  render: h => h(App),
  beforeCreate() {
    Vue.prototype.$bus = this
  }
}).$mount('#app')

```

step 2，发送方自定义事件中写入`this.$bus.$emit("Mes", this.msg)`

step 3，接收方在mounted钩子中，定义`this.$bus.$on("Mes", (msg) => {this.msg = msg})`

step 4，最好在beforeDestroy钩子中解绑事件`this.$bus.$off("Mes")`。



## 1.4 消息订阅与发布（pubsub）

1.   一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：```npm i pubsub-js```

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！

      ```js
      methods(){
        demo('xxx',data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：```pubsub.publish('xxx',数据)```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(this.pid)```去<span style="color:red">取消订阅。</span>

=======

>>>>>>> a8ec41daba2703ce0946b8ecf4b83cda070af108
