# Vue.use()是干嘛的

官方对 Vue.use() 方法的说明：通过全局方法 Vue.use() 使用插件，Vue.use 会自动阻止多次注册相同插件，它需要在你调用 new Vue() 启动应用之前完成。

Vue.use() 方法至少传入一个参数，该参数类型必须是 Object 或 Function。

如果是 Object 那么这个 Object 需要定义一个 install 方法，如果是 Function 那么这个函数就被当做 install 方法。