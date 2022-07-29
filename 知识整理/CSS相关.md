# CSS3新特性

## CSS3边框

- border-radius

- box-shadow

  该属性可设置的值包括阴影的 X 轴偏移量、Y 轴偏移量、模糊半径、扩散半径和颜色。

  模糊半径(blur-radius):(0,++)值越大，模糊面积越大，阴影越大越淡。

  扩散半径(spread-radius):(--,++)取负值，阴影收缩；取正值阴影扩大。需要考虑inset。

- border-image

  可设置的值：source slice width outset repeat | initial | inherit;

## CSS3 背景

- background-image

  如：background-image: url(img_flwr.gif)

  CSS3 允许你在元素上添加多个背景图像。

- background-size

- background-origin

  background-origin 属性指定了背景图像的位置区域。

  content-box, padding-box,和 border-box区域内可以放置背景图像。

- background-clip

  CSS3中background-clip背景剪裁属性是从指定位置开始绘制。区域同origin选项。

```css
//渐变：
线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
径向渐变（Radial Gradients）- 由它们的中心定义
background-image: linear-gradient(direction, color-stop1, color-stop2, ...);
```

## CSS3文本效果

- text-shadow
- box-shadow
- text-overflow：clip；ellipsis
- word-wrap
- word-break：keep-all；break-all（有连字符；无）

## CSS3字体

使用以前 CSS 的版本，网页设计师不得不使用用户计算机上已经安装的字体。使用 **CSS3**，网页设计师可以使用他/她喜欢的任何字体。只需简单的将字体文件包含在网站中，它会自动下载给需要的用户。您"自己的"的字体是在 **CSS3 @font-face** 规则中定义的。

在新的 @font-face 规则中，您必须首先定义字体的名称（比如 myFirstFont），然后指向该字体文件。

如：

```CSS
<style> 
@font-face
{
    font-family: myFirstFont;
    src: url(sansation_light.woff);
}
 
div
{
    font-family:myFirstFont;
}
</style>
```

## CSS3转换

CSS3 转换可以对元素进行移动、缩放、转动、拉长或拉伸。

### 2D转换

transform:如下属性

- translate()

  translate(x,y)方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。正值：→↓

- rotate()

  rotate(**deg)方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。

- scale()

  scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数

- skew()

  skew(**deg)包含两个参数值，分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。

  - skewX(<angle>);表示只在X轴(水平方向)倾斜。
  - skewY(<angle>);表示只在Y轴(垂直方向)倾斜。

- matrix()

  matrix()方法和2D变换方法合并成一个。

  matrix 方法有六个参数，包含旋转，缩放(2个)，移动（2个）和倾斜功能。

### 3D转换

transform:如下属性

- rotateX()

  rotateX()方法，围绕其在一个给定度数X轴旋转的元素。

- rotateY()

  rotateY()方法，围绕其在一个给定度数Y轴旋转的元素。

## CSS3过渡

CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。

所有属性

```css
div {
  transition-property: width;(all/property)
  transition-duration: 1s;
  transition-timing-function: linear;(ease;ease-in;ease-out;ease-in-out;cubic-                                       bezier(n,n,n,n))
  transition-delay: 2s;
}

```

## CSS3动画

@keyframes 规则是创建动画。@keyframes 规则内指定一个 CSS 样式和动画将逐步从目前的样式更改为新的样式。

```css
@keyframes myfirst
{
    0%   {background: red; left:0px; top:0px;}
    25%  {background: yellow; left:200px; top:0px;}
    50%  {background: blue; left:200px; top:200px;}
    75%  {background: green; left:0px; top:200px;}
    100% {background: red; left:0px; top:0px;}
}
div {
    animation-name: myfirst;
    animation-duration: 5s;
    animation-timing-function: linear;
    animation-delay: 2s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-play-state: running;
}
 
```

## CSS3 多列

## CSS3用户界面

- resize
- box-sizing
- outline-offset

## CSS3图片

滤镜：

CSS `filter` 属性用为元素添加可视效果 (例如：模糊与饱和度) 。

具体配置：https://www.runoob.com/cssref/css3-pr-filter.html

## CSS3 弹性盒子(Flex Box)

### 父元素：六个属性

主轴方向：flex-direction:       `row | row-reverse | column | column-reverse;`

如何换行：flex-wrap:          `nowrap | wrap | wrap-reverse;`

flex-flow:      `<flex-direction> || <flex-wrap>;`

主轴对齐方式：justify-content:      `flex-start | flex-end | center | space-between | space-around;`

副轴对齐方式：align-items:       `flex-start | flex-end | center | baseline | stretch;`

align-content: 定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

 `flex-start | flex-end | center | space-between | space-around | stretch;`

### 子元素：六个属性

order；flex-grow；flex-shrink；flex-basis；flex；align-self

```css
 flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
```

```css
 align-self: auto | flex-start | flex-end | center | baseline | stretch;
```

Grid栅格布局等

## CSS3 多媒体查询

媒体查询可用于检测很多事情，例如：

- viewport(视窗) 的宽度与高度
- 设备的宽度与高度
- 朝向 (智能手机横屏，竖屏) 。
- 分辨率

# CSS网格布局



# CSS权重

为 style 属性添加 1000，为每个 ID 添加 100，为每个属性、类或伪类添加 10，为每个元素名称或伪元素添加 1。此外，*通用选择器、被继承的值为0。

# CSS选择器常见的有哪几种?

### ![image-20220712163820862](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220712163820862.png)

![image-20220712163908993](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220712163908993.png)

# 伪类和伪元素的区别

伪类是选择器的一种，它用于选择处于特定状态的元素，比如当它们是这一类型的第一个元素时，或者是当鼠标指针悬浮在元素上面的时候。

它们表现得会像是你向你的文档的某个部分应用了一个类一样，帮你在你的标记文本中减少多余的类，让你的代码更灵活、更易于维护。

伪类就是开头为冒号的关键字：

```css
:pseudo-class-name
```

伪元素以类似方式表现，不过表现得是像你往标记文本中加入全新的 HTML 元素一样，而不是向现有的元素上应用类。伪元素开头为双冒号`::`。

```css
::pseudo-element-name
```

区别：伪类和伪元素的区别，最关键的点在于如果没有伪元素(或伪类)，**是否需要添加元素才能达到目的**，如果是则是伪元素，反之则是伪类。



# *position

方式：static、relative、absolute 、fixed、 sticky

## relative VS absolute

`relative`表示，相对于默认位置（即`static`时的位置）进行偏移，即定位基点是元素的默认位置。(仍在文档流中)

`absolute`表示，相对于上级元素（一般是父元素）进行偏移，即定位基点是父元素。

限制条件：定位基点（一般是父元素）不能是`static`定位，否则定位基点就会变成整个网页的根元素`html`。

注意，`absolute`定位的元素会被"正常页面流"忽略，“脱标”。即在"正常页面流"中，该元素所占空间为零，周边元素不受影响。

relative、absolute 、fixed。这三种定位都不会对其他元素的位置产生影响，因此元素之间可能产生重叠。

## fixed

`fixed`表示，相对于视口（viewport，浏览器窗口）进行偏移，即定位基点是浏览器窗口。这会导致元素的位置不随页面滚动而变化，好像固定在网页上一样。

##  sticky

粘性元素根据滚动位置在相对（relative）和固定（fixed）之间切换。起先它会被相对定位，直到在视口中遇到给定的偏移位置为止 - 然后将其“粘贴”在适当的位置。

因此，它能够形成"动态固定"的效果。比如，网页的搜索工具栏，初始加载时在自己的默认位置（`relative`定位）。页面向下滚动时，工具栏变成固定位置，始终停留在页面头部（`fixed`定位）。

应用：堆叠效果；表头锁定。

# rem、em、px

px像素（Pixel）。绝对长度单位。

em，相对长度单位。

- 子元素字体（font-size）大小的em是相对于父元素字体大小
- 元素的width/height/padding/margin用em的话是相对于该元素的font-size

rem，相对长度单位，相对于根元素（html标签）的字体大小。

# 可替换元素和不可替换元素

元素是文档结构的基础，在`CSS`中，每个元素生成了一个包含了元素内容的框（`box`，也译为“盒子”）。但是不同的元素显示的方式会有所不同，例如`<div>`和`<span>`就不同，而`<strong>`和`<p>`也不一样。在文档类型定义（DTD）中对不同的元素规定了不同的类型，这也是DTD对文档之所以重要的原因之一。

从元素本身的特点来讲，可以分为可替换元素(replaceable element)和不可替换元素(none-replaceable element)。

## 可替换元素

*可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。*

> 例如浏览器会根据`<img>`标签的`src`属性的值来读取图片信息并显示出来，而如果查看`(x)html`代码，则看不到图片的实际内容；又例如根据`<input>`标签的`type`属性来决定是显示输入框，还是单选按钮等。

*`(x)html`中的`<img>`、`<input>`、`<textarea>`、`<select>`、`<object>`都是替换元素。这些元素往往没有实际的内容，即是一个空元素。*

## 不可替换元素

`(x)html` 的大多数元素是不可替换元素，*即其内容直接表现给用户端（例如浏览器）*。

> 例如：`<p>段落的内容</p>`
> 段落<p>是一个不可替换元素，文字“段落的内容”全被显示。

https://segmentfault.com/a/1190000006835284

# Doctype

在 [HTML](https://developer.mozilla.org/zh-CN/docs/Glossary/HTML) 中，文档类型 doctype 的声明是必要的。在所有文档的头部，你都将会看到"`<!DOCTYPE html>`" 的身影。这个声明的目的是防止浏览器在渲染文档时，切换到我们称为“[怪异模式 (兼容模式)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)”的渲染模式。“`<!DOCTYPE html>`" 确保浏览器按照最佳的相关规范进行渲染，而不是使用一个不符合规范的渲染模式。

# *opacity VS RGBA

**opacity** ：所有子元素都继承相同的透明度。这可能会使完全透明的元素内的文本难以阅读。

RGBA的子元素不继承透明度。

opacity取值范围为 0.0 - 1.0。值越低，越透明。RGBA：rgba(*red*, *green*, *blue*, *alpha*)。*alpha* 参数是介于 0.0（完全透明）和 1.0（完全不透明）之间的数字。

# *水平垂直居中方法

## 水平

**水平居中**可分为**行内元素水平居中**和**块级元素水平居中**

### 行内元素

文本text、图像img、按钮超链接等。父元素设置`text-align:center`。

### 块级元素

①定宽：该元素加`margin:0 auto`，**注意，块状元素有width值且不为100%**

②不定宽：

该元素设置`display:table`，`margin:0 auto`来实现。

子元素设置`inline-block`，同时<font color='red'>父元素</font>设置`text-align:center`。

父元素设置`display:flex,justify-content:center;`

`position + 负margin`//////////`position + margin：auto`；///////////`position + transform`；

## 垂直

### 单行文本：

设置`paddingtop=paddingbottom`；或

设置`line-height=height`；

### 多行文本：

<font color='red'>子元素</font>设置`vertical-align:middle`。

### 块级元素：

父元素设置`display:flex`和`align-items：center`。父元素必须显示设置height值。

`position + 负margin`//////////`position + margin：auto`；///////////`position + transform`；

## 水平垂直居中

1.**绝对定位+margin:auto**          

```css
div{
    width: 200px;
    height: 200px;
    background: green;
    
    position:absolute;
    left:0;
    top: 0;
    bottom: 0;
    right: 0;
    margin: auto;
}
```

2.**绝对定位+负margin**

```css
div{
    width:200px;
    height: 200px;
    background:green;
    
    position: absolute;
    left:50%;
    top:50%;
    margin-left:-100px;
    margin-top:-100px;
}
```

3.**绝对定位+transform**

```css
div{
    width: 200px;
    height: 200px;
    background: green;
    
    position:absolute;
    left:50%;    /* 定位父级的50% */
    top:50%;
    transform: translate(-50%,-50%); /*自己的50% */
}
```

4.**flex布局**    

```css
.box{
   height:600px;   
   display:flex;
   justify-content:center;  //子元素水平居中
   align-items:center;      //子元素垂直居中
   /* aa只要三句话就可以实现不定宽高水平垂直居中。 */
}
.box>div{
    background: green;
    width: 200px;
    height: 200px;
}
```

# *border-style设置1-4个值

1：所有边框。2：上下；左右。3：上；右左；下。4：上；右；左；下。

border-width 和 border-color 也同样适用。

border-radius、margin、padding

# *CSS简写

background: color image repeat attachment position; 

你可以省略其中一个或多个属性值，如果省略，该属性值将用浏览器默认值，默认值为：

color: transparent      image: none            repeat: repeat            attachment: scroll                   position: 0% 0%

border: width style color;

font: font-style font-weight  font-size/line-height font-family

```css
/* x 偏移量 | y 偏移量 | 阴影模糊半径 | 阴影扩散半径 | 阴影颜色 */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
```

**模糊半径就是渐变阴影半径，而扩散半径就是纯色阴影半径**。并且，渐变阴影包在扩散阴影外面。

# 元素的显示和隐藏

| 显示隐藏方式                     | 是否占据空间      | 是否导致浏览器重排重绘     | 能否触发点击事件 |
| -------------------------------- | ----------------- | -------------------------- | ---------------- |
| display : none                   | 不占空间          | 是                         | 否               |
| visibility : hidden              | 占空间            | 否                         | 否               |
| opacity : 0                      | 占空间            | 否                         | 是               |
| 设置height，width等盒模型属性为0 | 设置为0后不占空间 | 可能会导致浏览器重排和重绘 | 否               |

# 重排与重绘

## 页面生成的过程：

1.HTML 被 HTML 解析器解析成 DOM 树；

2.CSS  被 CSS 解析器解析成 CSSOM 树；

3.结合 DOM 树和 CSSOM 树，生成一棵渲染树(Render Tree)，这一过程称为 Attachment；

4.生成布局(flow)，浏览器在屏幕上“画”出渲染树中的所有节点；

5.将布局绘制(paint)在屏幕上，显示出整个页面。

第四步和第五步是最耗时的部分，这两步合起来，就是我们通常所说的渲染。

## 渲染：

在页面的生命周期中，**网页生成的时候，至少会渲染一次。在用户访问的过程中，还会不断触发重排(reflow)和重绘(repaint)**，不管页面发生了重绘还是重排，都会影响性能，最可怕的是重排，会使我们付出高额的性能代价，所以我们应尽量避免。

- 重绘：某些元素的外观被改变，例如：元素的填充颜色
- 重排：重新生成布局，重新排列元素。

## 重排(reflow)：

### 概念：

当DOM的变化影响了元素的几何信息(元素的的位置和尺寸大小)，浏览器需要重新计算元素的几何属性，将其安放在界面中的正确位置，这个过程叫做重排。

重排也叫回流，简单的说就是重新生成布局，重新排列元素。

### 触发重排：

- 页面初始渲染，这是开销最大的一次重排
- 添加/删除可见的DOM元素
- 改变元素位置
- 改变元素尺寸，比如边距、填充、边框、宽度和高度等
- 改变元素内容，比如文字数量，图片大小等
- 改变元素字体大小
- 改变浏览器窗口尺寸，比如resize事件发生时
- 激活CSS伪类（例如：`:hover`）
- 设置 style 属性的值，因为通过设置style属性改变结点样式的话，每一次设置都会触发一次reflow
- 查询某些属性或调用某些计算方法：offsetWidth、offsetHeight等，除此之外，当我们调用 `getComputedStyle`方法，或者IE里的 `currentStyle` 时，也会触发重排，原理是一样的，都为求一个“即时性”和“准确性”。

### 重排影响的范围：

由于浏览器渲染界面是基于流式布局模型的，所以触发重排时会对周围DOM重新排列，影响的范围有两种：

- 全局范围：从根节点html开始对整个渲染树进行重新布局。
- 局部范围：对渲染树的某部分或某一个渲染对象进行重新布局。

## 重绘(Repaints):

### 概念：

当一个元素的外观发生改变，但没有改变布局,重新把元素外观绘制出来的过程，叫做重绘。

### 常见的引起重绘的属性：

| 属性：          | --               | --                  | --                |
| --------------- | ---------------- | ------------------- | ----------------- |
| color           | border-style     | visibility          | background        |
| text-decoration | background-image | background-position | background-repeat |
| outline-color   | outline          | outline-style       | border-radius     |
| outline-width   | box-shadow       | background-size     |                   |

## 重排优化建议：

重排的代价是高昂的，会破坏用户体验，并且让UI展示非常迟缓。通过减少重排的负面影响来提高用户体验的最简单方式就是尽可能的减少重排次数，重排范围。下面是一些行之有效的建议，大家可以用来参考。

### 减少重排范围

我们应该尽量以局部布局的形式组织html结构，尽可能小的影响重排的范围。

- 尽可能在低层级的DOM节点上，而不是像上述全局范围的示例代码一样，如果你要改变p的样式，class就不要加在div上，通过父元素去影响子元素不好。
- 不要使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局。那么在不得已使用table的场合，可以设置table-layout:auto;或者是table-layout:fixed这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围。

### 减少重排次数

#### 1.样式集中改变

不要频繁的操作样式，对于一个静态页面来说，明智且可维护的做法是更改类名而不是修改样式，对于动态改变的样式来说，相较每次微小修改都直接触及元素，更好的办法是统一在 `cssText` 变量中编辑。虽然现在大部分现代浏览器都会有 `Flush` 队列进行渲染队列优化，但是有些老版本的浏览器比如IE6的效率依然低下。

#### 2.分离读写操作

DOM 的多个读操作（或多个写操作），应该放在一起。不要两个读操作之间，加入一个写操作。

#### 3.将 DOM 离线

“离线”意味着不在当前的 DOM 树中做修改，我们可以这样做：

- 使用 display:none

  一旦我们给元素设置 `display:none` 时（只有一次重排重绘），元素便不会再存在在渲染树中，相当于将其从页面上“拿掉”，我们之后的操作将不会触发重排和重绘，添加足够多的变更后，通过 `display`属性显示（另一次重排重绘）。通过这种方式即使大量变更也只触发两次重排。另外，`visibility : hidden` 的元素只对重绘有影响，不影响重排。

- 通过 [documentFragment](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FDocumentFragment) 创建一个 `dom` 碎片,在它上面批量操作 `dom`，操作完成之后，再添加到文档中，这样只会触发一次重排。

- 复制节点，在副本上工作，然后替换它！

#### 4.使用 absolute 或 fixed 脱离文档流

使用绝对定位会使的该元素单独成为渲染树中 `body` 的一个子元素，重排开销比较小，不会对其它节点造成太多影响。当你在这些节点上放置这个元素时，一些其它在这个区域内的节点可能需要重绘，但是不需要重排。

#### 5.优化动画

- 可以把动画效果应用到 `position`属性为 `absolute` 或 `fixed` 的元素上，这样对其他元素影响较小。

  动画效果还应牺牲一些平滑，来换取速度，这中间的度自己衡量： 比如实现一个动画，以1个像素为单位移动这样最平滑，但是Layout就会过于频繁，大量消耗CPU资源，如果以3个像素为单位移动则会好很多

- 启用GPU加速 `GPU` 硬件加速是指应用 `GPU` 的图形性能对浏览器中的一些图形操作交给 `GPU` 来完成，因为 `GPU` 是专门为处理图形而设计，所以它在速度和能耗上更有效率。

  `GPU` 加速通常包括以下几个部分：Canvas2D，布局合成, CSS3转换（transitions），CSS3 3D变换（transforms），WebGL和视频(video)。

# *display:none VS visibility:hidden

display:none:隐藏，不占有原来位置。页面将显示为好像该元素不在其中。

visibility:hidden:隐藏。占用与之前相同的空间。

# *外边距合并

当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于外边距高度中的较大者。

当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分隔开），它们的上和/或下外边距也会发生合并。

**注释：**只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。

# *浮动与清除浮动

## 浮动特性

**浮动元素会脱离文档流并向左/向右浮动，直到碰到父元素或者另一个浮动元素**。

导致的问题：浮动元素脱离了文档流，不占据文档流的位置，父元素不能被撑开，高度没了。

```css
// css
.box-wrapper {
  border: 5px solid red;
}
.box-wrapper .box {
  float: left; 
  width: 100px; 
  height: 100px; 
  margin: 20px; 
  background-color: green;
}

// html
<div class="box-wrapper">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

![img](https://upload-images.jianshu.io/upload_images/1158202-62ba6cdb840c8262.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

## 清除浮动

给父元素设定高度可以消除浮动造成的影响，但实际业务往往不允许给父元素设定高度。

### clear清除浮动

原理：clear属性规定元素的(left,right,both)侧不允许其他浮动元素。

方法：①添加新的块级元素，写入clear属性（页面中增加冗余标签，违背了语义网的原则。）

```css
<div class="box-wrapper">
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div style="clear:both;"></div>
</div>
```

②添加伪元素

```css
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}
```

更通用的实现代码:

```css
/* For modern browsers */
.cf:before,
.cf:after {
　　content:"";
　　display:block;
}

.cf:after {
　　clear:both;
}

/* For IE 6/7 (trigger hasLayout) */
.cf {
　　zoom:1;
}
```



### BFC清除浮动

#### 定义

BFC（Block Formatting Context）块格式化上下文，是盒模型的一种渲染布局，简言之可以理解为 **一个独立的容器，不受外部影响，不影响外部。**

#### 形成条件

1. 固定(fixed)定位和绝对(absolute)定位
2. float:both,left,right(除了none)
3. overflow:hidden,auto,scroll(除了visible)
4. display:inline-block,table-cell,table-caption

#### 特点

1. BFC 是页面上的一个独立容器，容器里面的子元素不会影响外面的元素。
2. BFC 内部的块级盒会在垂直方向上一个接一个排列
3. 同一 BFC 下的相邻块级元素可能发生外边距折叠，创建新的 BFC 可以避免外边距折叠
4. 每个元素的外边距盒（margin box）的左边与包含块边框盒（border box）的左边相接触（从右向左的格式的话，则相反），即使存在浮动
5. 浮动盒的区域不会和 BFC 重叠
6. 计算 BFC 的高度时，浮动元素也会参与计算

#### 作用

1. **清除浮动**：BFC会包含创建它的元素内部的所有内容（包含浮动元素）
2. **外边距折叠**：解决同一BFC容器中的相邻元素间的外边距折叠问题
3. **左图右文布局**：浮动盒的区域不会和 BFC 重叠

# 盒模型

box-sizing:content-box[标准盒模型-w3c盒模型]

box-sizing:border-box[IE盒模型-怪异盒模型]因为低版本IE中，元素盒子的box-sizing默认是border-box

- `content-box` 是默认值。content-box中，属性width，height只包含内容content，不包含border和padding。内容（content）在CSS中其主要作用的属性是width和height。
- `border-box` border-box中，属性width，height则包含content、border和padding。大多数情况下，这使得我们更容易地设定一个元素的宽高。



# 画一个三角形

```css
#triangle02{
    width: 0;
    height: 0;
    border-top: 50px solid blue;
    border-right: 50px solid red;
    border-bottom: 50px solid green;
    border-left: 50px solid yellow;
    }
```

![image-20220729211959885](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220729211959885.png)

```css
#triangle03{
    width: 0;
    height: 0;
    border: 50px solid transparent;
    border-top: 50px solid blue;
    }
#triangle04{
    width: 0;
    height: 0;
    border: 50px solid transparent;
    border-right: 50px solid red;
    }
#triangle05{
    width: 0;
    height: 0;
    border: 50px solid transparent;
    border-bottom: 50px solid green;
    }
#triangle06{
    width: 0;
    height: 0;
    border: 50px solid transparent;
    border-left: 50px solid yellow;
    }
```

![image-20220729212050998](C:\Users\14211\AppData\Roaming\Typora\typora-user-images\image-20220729212050998.png)

# 其他

margin 属性设置为 auto，以使元素在其容器中水平居中。

margin允许负值，padding不允许负值。

text-align 属性用于设置文本的水平对齐方式(left,center,right)。vertical-align 属性设置元素的垂直对齐方式(top,middle,bottom)。