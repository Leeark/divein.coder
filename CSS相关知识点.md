# CSS权重

为 style 属性添加 1000，为每个 ID 添加 100，为每个属性、类或伪类添加 10，为每个元素名称或伪元素添加 1。此外，*通用选择器、被继承的值为0。

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

# Flex布局

## 父元素：六个属性

主轴方向：flex-direction:       `row | row-reverse | column | column-reverse;`

如何换行：flex-wrap:          `nowrap | wrap | wrap-reverse;`

flex-flow:      `<flex-direction> || <flex-wrap>;`

主轴对齐方式：justify-content:      `flex-start | flex-end | center | space-between | space-around;`

副轴对齐方式：align-items:       `flex-start | flex-end | center | baseline | stretch;`

align-content: 定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

 `flex-start | flex-end | center | space-between | space-around | stretch;`

## 子元素：六个属性

order；flex-grow；flex-shrink；flex-basis；flex；align-self

```css
 flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
```

```css
 align-self: auto | flex-start | flex-end | center | baseline | stretch;
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

# 其他

margin 属性设置为 auto，以使元素在其容器中水平居中。

margin允许负值，padding不允许负值。

text-align 属性用于设置文本的水平对齐方式(left,center,right)。vertical-align 属性设置元素的垂直对齐方式(top,middle,bottom)。

box-sizing:content-box

box-sizing:border-box

- `content-box` 是默认值。如果你设置一个元素的宽为100px，那么这个元素的内容区会有100px 宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。
- `border-box` 告诉浏览器：你想要设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px，那么这100px会包含它的border和padding，内容区的实际宽度是width减去(border + padding)的值。大多数情况下，这使得我们更容易地设定一个元素的宽高。