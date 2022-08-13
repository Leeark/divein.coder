# HTML5新特性

1.语义化标签

2.增强型表单包括属性以及元素

3.新增视频<video>和音频<audio>标签

4.Canvas 图形

5.SVG绘图

6.地理定位

7.拖放API

8.Web Worker

9.Web Storage

10.Web Socket

# meta标签有哪些属性；

<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。

![image-20220711140221960](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220711140221960.png)

# script标签有哪些属性；

![image-20220711143718864](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220711143718864.png)

# HTML基本结构存在哪些标签；

1. ```html
    <!DOCTYPE html>
   <html>
    <head>
     <title>Document</title>
    </head>
   <body>
   </body>
   </html>
   ```

   

# HTML语义化

# 可以控制script标签加载顺序吗

script 标签有2个属性 async（异步） 和 defer（推迟）；他们的功能是：

总结:都用于外部脚本  async异步下载完立即执行  defer异步下载完等dom加载完成后执行  

兼容性问题script标签放最底下

async：他是异步加载，不确定何时会加载好；页面加载时，带有 async 的脚本也同时加载，加载后会立即执行。

如果有一些需要操作 DOM 的脚本加载比较慢时，这样会造成 DOM 还没有加载好，脚本就进行操作，会造成错误。

defer：页面加载时，带有 defer 的脚本也同时加载，加载后会等待 页面加载好后，才执行。



