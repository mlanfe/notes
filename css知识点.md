## 前言

值得扩展的我都在问题后面附上文章链接，里面会有详细的讲解和案例分析，面试突击的话只看本文就好了，想跟面试官聊聊技术的可以深入的看一下。

最后，整理不易，所以。。如果白嫖使你快乐的话。。。。那就白嫖吧。。。但是，不点赞的话，以后找不到了哦🤔🤔

## 标准的CSS盒子模型及其和低版本的IE盒子模型的区别？

标准盒模型(`content-box`)：width = 内容宽度（content） + border + padding + margin

低版本IE盒子模型(`border-box`)： width = 内容宽度（content + border + padding）+ margin

区别： 标准盒子模型盒子的`height`和`width`是`content`的宽高，而IE盒子模型盒子的宽高则包括`content+padding+border`部分。

## CSS优先级算法如何计算？

```
！important  >   内联样式   >   id   >   class   >   标签   >   通配符   >   继承   >   默认
```

#### **权重计算**

把特殊性分为4个等级，每个等级代表一类选择器，每个等级的值为其所代表的选择器的个数乘以这一等级的权值，最后把所有等级的值相加得出选择器的特殊值。

4个等级的定义如下：

> 假设第零等：!important 权值10000 第一等：代表内联样式，如: style=””，权值为1000。 第二等：代表ID选择器，如：#content，权值为0100。 第三等：代表类，伪类和属性选择器，如.content，权值为0010。 第四等：代表标签选择器和伪元素选择器，如div p，权值为0001。 第五等：通用选择器（*），子选择器（>），相邻同胞选择器（+），权值为0000 示例如下：

```
**注意** 数位之间没有进制 比如说： 0,0,0,5 + 0,0,0,5 =0,0,0,10 而不是 0,0, 1, 0
#header #left ul li .first a {...}
  100.   100  1  1.  10    1
---> sum 0213
复制代码
```

1. 权重相同，写在后面的会覆盖前面的
2. 权重相同，一个在写在外部样式中`link`引入，另一个在内部样式`style`引入，引入顺序后面的覆盖前面的
3. 内联样式的权重为1,0,0,0，10个id选择器的权重也为0,10,0,0，内联样式优先级高

## 如何居中div？

> ps: 选中下列样例可在控制台直接调试，纯手工打造，作者诚意很足的

使用下列样式：

#### 1、margin: 0 auto;

要求目标元素宽度固定，并且与父元素左右margin有空余。

> 适用于父元素内有多个块级元素上下排列的情况

```html
<div class="container">
  this is inner text
  <div classs="ele2">
      this is another block element
  </div>
</div>
复制代码
.container{
  width: 300px;
  border: 1px solid grey;
  text-align: center;
}
.ele2{
  border: 1px solid grey;
  width: 200px;
  margin:0 auto;
}
复制代码
```

  this is inner text  

​      this is another block element  

> 如果上下的margin设置了auto，其计算值为0

#### 2、absolute + transform

transform设置百分比参数是相对于自身尺寸的

```html
<div class="container">
   this is inner text
  <div class="ele1">
    this is a block element
  </div>
</div>
复制代码
.container{
    height: 100px;
    width: 200px;
    position: relative;
    border: 1px solid grey;
  	text-align: center;
}
.ele1{
    position: absolute;
    left: 50%;
    transform: translateX(-50%);  
    width: 100px; // 此处可以不设置，默认为父元素一半宽度
    border: 1px solid #888;
}
复制代码
```

   this is inner text  

​    this is a block element  

> ele1可以不设定width的值，此时ele1的宽度会被计算为 `父元素的一半 - 左右边框的宽度`

#### 3、 absolute + margin

margin设置百分比参数是相对于父元素的，所以，此方法需要子元素**固定宽度**，并且值设为自身宽度的一半；

html代码同上，替换 `ele1` 元素样式中  `transform: translateX(-50%)` 为 `margin-left: -50px;`

```css
.ele1{
    position: absolute;
    left: 50%;
    margin-left: -50px; // 负值，设为元素自身宽度的一半
    width: 100px; // 此处必须设置
    border: 1px solid #888;
}
复制代码
```

   this is inner text  

​    this is a block element  

#### 4、 flex

```
这个不用叙述了吧  
复制代码
```

#### 5、 absolute + margin: auto

```
适用于垂直居中
复制代码
```

更多布局请移步[可食用的「css布局干货」 | 水平、垂直、多列](https://juejin.im/post/6844904164435181581)，
 条理清晰的列举了水平及垂直居中，手打示例，可在页面调试

## display有哪些值？他们的作用是什么？

| 值                 | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| none               | 使用后元素将不会显示                                         |
| block              | 使用后元素将变为块级元素显示，元素前后带有换行符             |
| inline             | display默认值。使用后原色变为行内元素显示，前后无换行符      |
| list-item          | 使用后元素作为列表显示                                       |
| run-in             | 使用后元素会根据上下文作为块级元素或行内元素显示             |
| table              | 使用后将作为块级表格来显示（类似`<table>`），前后带有换行符  |
| inline-table       | 使用后元素将作为内联表格显示（类似`<table>`），前后没有换行符 |
| table-row-group    | 元素将作为一个或多个行的分组来显示（类似`<tbody>`）          |
| table-header-group | 元素将作为一个或多个行的分组来表示（类似`<thead>`）          |
| table-footer-group | 元素将作为一个或多个行分组显示（类似`<tfoot>`）              |
| table-row          | 元素将作为一个表格行显示（类似`<tr>`）                       |
| table-column-group | 元素将作为一个或多个列的分组显示（类似`<colgroup>`）         |
| table-column       | 元素将作为一个单元格列显示（类似`<col>`）                    |
| table-cell         | 元素将作为一个表格单元格显示（类似`<td>和<th>`）             |
| table-caption      | 元素将作为一个表格标题显示（类似`<caption>`）                |
| inherit            | 规定应该从父元素集成display属性的值                          |

## position不同的值的定位原点及其特性？

`relative`（相对定位）： 生成相对定位的元素，定位原点是元素本身所在的位置，在原本文档流位置占据一定空间；

`absolute`（绝对定位）：生成绝对定位的元素，定位原点是最近的position`设置为`absolute`或者`relative`的父元素的左上角。

`fixed` （老IE不支持）：生成绝对定位的元素，相对于浏览器窗口进行定位，元素会被移出正常文档流，并不为元素预留空间。

`static`：默认值。没有定位，元素出现在正常的流中（忽略 `top`, `bottom`, `left`, `right`、`z-index` 声明）。

`inherit`：从父元素继承 `position` 属性的值。

`sticky`：元素根据正常文档流进行定位，可以被认为是相对定位和固定定位的混合。当元素在屏幕或滚动元素显示区域时，表现为relative，就要滚出显示器屏幕的时候，表现为fixed。可用来做吸顶特效，详见[css position属性及其sticky属性值的特性](https://juejin.im/post/6844904159292948493)

## 如何用纯CSS创建一个三角形

> ps: 选中下列样例可在控制台直接调试，纯手工打造，作者诚意很足的

块级元素宽高设为0，仅设置某一条边的颜色，另外三条边颜色设定为（transparent）

```html
<div class="container">
  <div class="triangle-top"></div>
   <div class="triangle-left"></div>
   <div class="triangle-right"></div>
   <div class="triangle-bottom"></div>
</div>
复制代码
.container{
  display: flex;
  justify-content: space-between;
  width: 400px;
}
.container div{
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent;
}
.container .triangle-top {
    border-bottom-color: orange; 
}
.container .triangle-left {
    border-right-color: orange; 
}
.container .triangle-right {
    border-left-color: orange; 
}
.container .triangle-bottom {
    border-top-color: orange; 
}
复制代码
```

> 记得使用相对定位居中箭头

## 浮动原理及什么时候需要清除浮动？清除浮动的方式？

### 什么是浮动

元素加了浮动后，会脱离文档流，提升了半层层级，向着指定方向移动，直到遇到父元素的边界或另一个浮动元素停止

### 什么是层级

如果将整个元素看做一层，则下半层是元素本身（背景样式等），上半层是元素中的内容

**举例**

```html
<div class="container">
  <div class="box1">box1</div>
   <div class="box2">box2</div>
   <div class="box3">box3</div>
</div>
复制代码
.container{
 width: 40px;
 border: 1px solid black;
}
.container div{
  width: 100%;
  height: 30px;
}
.box1 {
  background: yellow;
}
.box2 {
    background: orange; 
}
.box3 {
     background: pink; 
}
复制代码
```

三个盒子都没有浮动时

box1

box2

box3

当给box2添加float:left时，三个盒子的排列变成

box1

box2

box3

此时由于box2浮动脱离了文档流，box3上移，被box2遮挡了。但此时box3盒子里的文字box3并没有上移！！！

**小知识**

1. 浮动元素之间是漂浮着，并不会形成一个流。浮动元素总是要保证自己的顶部与上一个标准流中的元素（未浮动元素）的底部对齐。
2. position：absolute和float会隐式地改变display类型，除display:none外，只要设置了position：absolute或float，都会让元素以display:inline-block的方式显示，可以设置长宽

浮动会带来的问题：

1.影响兄弟元素的位置

2.使父元素产生高度塌陷

### 清除浮动造成的缺陷的方式：

- 父级盒子定义高度（height）;
- 最后一个浮动元素后面加一个div空标签，并且添加样式clear: both;
- 包含浮动元素的父级标签添加样式overflow为hidden/both;
- 父级div定义zoom;

### 清除浮动的实质

1. 利用css的clear属性，加clear:both
2. 触发浮动元素父元素的BFC，使该父元素可以包含浮动元素

## CSS预处理器/后处理器是什么？为什么要使用它们？

**什么是CSS 预处理器？**
 CSS 预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为 CSS 增加了一些编程的特性，将 CSS 作为目标生成文件，然后开发者就只要使用这种语言进行CSS的编码工作。

**为什么要使用CSS预处理器？**

CSS仅仅是一个标记语言，不可以自定义变量，不可以引用。

如：less，sass，stylus,用来预编译sass或者less，增加了css代码的复用性，还有层级，mixin， 变量，循环， 函数等，对编写以及开发UI组件都极为方便。

**CSS有具体以下几个缺点：**

- 语法不够强大，比如无法嵌套书写，导致模块化开发中需要书写很多重复的选择器；
- 没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护。

预编译很容易造成后代选择器的滥用

**使用预处理器的优点**

- 提供CSS层缺失的样式层复用机制
- 减少冗余代码
- 提高样式代码的可维护性

详细资料可以参考：【[Sass.vs.Less | 简介与比较](https://juejin.im/post/6844904169313140749)】

**后处理器** 是对 CSS 进行处理，并最终生成 CSS 的 预处理器，它属于广义上的 CSS 预处理器。 我们很久以前就在用 CSS 后处理器 了，最典型的例子是 CSS 压缩工具（如 clean-css），只不过以前没单独拿出来说过。
 还有最近比较火的 Autoprefixer，以 Can I Use 上的 浏览器支持数据 为基础，自动处理兼容性问题。

使用原因：

- 结构清晰， 便于扩展
- 可以很方便的屏蔽浏览器私有语法的差异
- 可以轻松实现多重继承

## ::before 和 :after中双冒号和单冒号有什么区别？

在 CSS 中伪类一直用单冒号 : 表示，如 :hover, :active 等

伪元素在CSS1中已存在，当时语法是用 : 表示，如 :before 和 :after，后来在CSS3中修订，为了区分伪元素和伪类，伪元素改用用 :: 表示，如 ::before 和 ::after。

> 由于低版本IE对双冒号不兼容，开发者为了兼容性各浏览器，继续使使用 :after 这种老语法表示伪元素。

想让插入的内容出现在其元素内容前，使用::before，否者，使用::after；

在代码顺序上，::after生成的内容也比::before生成的内容靠后。

如果按堆栈视角，::after生成的内容会在::before生成的内容之上

## 伪元素和伪类的区别

css引入伪类和伪元素概念是为了格式化文档树以外的信息。

- 伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定的元素时，我们可以通过:hover来描述这个元素的状态。虽然它和普通的css类相似，可以为已有的元素添加样式，但是它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。
- 伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如说，我们可以通过:before来在一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中。

**css伪类**

| 选择器     | 示例        | 示例说明               |
| ---------- | ----------- | ---------------------- |
| [:link]    | a:link      | 选择所有未访问链接     |
| [:visited] | a:visited   | 选择所有访问过的链接   |
| [:active]  | a:active    | 选择正在活动链接       |
| [:hover]   | a:hover     | 把鼠标放在链接上的状态 |
| [:focus]   | input:focus | 选择元素输入后具有焦点 |

**css伪元素**

| 选择器              | 示例           | 示例说明                                     |
| ------------------- | -------------- | -------------------------------------------- |
| [:first-letter]     | p:first-letter | 选择每个 元素的第一个字母                    |
| [:first-line]       | p:first-line   | 选择每个 元素的第一行                        |
| [:first-child]      | p:first-child  | 选择器匹配属于任意元素的第一个子元素的  元素 |
| [:before]           | p:before       | 在每个元素之前插入内容                       |
| [:after]            | p:after        | 在每个元素之后插入内容                       |
| [:lang(*language*)] | p:lang(it)     | 为元素的lang属性选择一个开始值               |

## rgba() 和 opacity 的透明效果有什么不同？

- `opacity` 作用于元素以及元素内的所有内容（包括文字）的透明度；
- `rgba()`只作用于元素自身的颜色或其背景色，子元素不会继承透明效果；

## css 属性 content 有什么作用？

content属性专门应用在 before/after 伪元素上，用来插入生成内容。最常见的应用是利用伪类清除浮动。

**扩展：如何通过css content属性实现css计数器？**

css计数器是通过设置counter-reset 、counter-increment 两个属性 、及 counter()/counters()一个方法配合after / before 伪类实现。

## px、em、rem有什么区别？

- `px`相对于显示器屏幕分辨率。

  **PX特点**

  - IE无法调整那些使用px作为单位的字体大小；
  - 国外的大部分网站能够调整的原因在于其使用了em或rem作为字体单位；
  - Firefox能够调整px和em，rem。

- em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

  **EM特点**

  - em的值并不是固定的；
  - em会继承父级元素的字体大小。

注意：任意浏览器的默认字体高都是16px。所有未经调整的浏览器都符合: 1em=16px。

- rem是CSS3新增的一个相对单位（root em，根em），这个单位与em区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。

目前，除了IE8及更早版本外，所有浏览器均已支持rem。

## 一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度问题怎么解决？

1. 使用`calc`

```css
.div1{
	height: 100px;
}
.div2 { 
	height: calc(100%-100px); 
}
复制代码
```

1. 绝对定位

```css
.container{
	position: relative;
}
.div1{
	height: 100px;
}
.div2 { 
	position: absolute;
	top: 100px;
  bottom: 0;
}
复制代码
```

1. `flex`布局

```css
.container { 
  display:flex; 
  flex-direction:column; 
} 
.div1{
	height: 100px;
}
.div2 { 
	flex:1; 
}
复制代码
```

## transition、transform和animation的区别

**Transform:**

transform属性是静态属性，一旦写到style里面，将会直接显示作用，无任何变化过程。transform的主要用途是用来做元素的特殊变形，它定义了元素静态样式中实现变形、旋转、缩放、移位及透视等功能。

**Transition**

transition属性是一个简单的动画属性，可以说它是animation的简化版本，是给普通做简单网页特效用的。

比如你有如下两个样式：

```
.position{
    left:100px;
    top:100px;
}
.position1{
    -webkit-transition:left 0.5s ease-out;
    left:500px;
    top:500px;
}
复制代码
```

元素的`class`类为`position`。当你将其`classList` 增加 `position1` 或者替换`position` 为`position1`的时候，元素的属性变化，触发webkit-transition，以指定属性变化前的值为起始值，变化后的属性为结束值，执行动画效果。这是一个简单的两点变化过程，大大简化了`animation`属性的复杂程度。

其中`position1`的`transition`的属性的意思说：当你的`left`属性发生变化的时候，执行动画效果（仅仅基于left的属性变化，其他的属性不会加入到动画变化里面去）；

> 在transtion属性里面指定响应属性为all，可以响应并执行元素所有属性的变化动画（能做动画的属性）。

**Animation:**

在官方的Introduction上介绍这个属性是transition属性的扩展。但是这个简单的介绍里面包含了不简单的东西：keyframes。

看一个简单的 keyframes 的示例：

```css
@keyframes 'wobble'{
  0%{
   left:100px
}
   30%{
   left:300px;
}
  100%{
   left:500px;
}
}
.animate{
left:100px;
   -webkit-animation:wobble 0.5s ease-out;
   -webkit-animation-fill-mode:backwards;
}
复制代码
```

上面这个代码展示了一个keyframes ‘wobble’，其中 0％ 代表在变化中不同时间点的属性值，你可以较精确的控制动画变化中任何一个时间点的属性效果。而animation则根据这个keyframes提供的属性变化方式去计算元素动画当中的属性。

它本身被用来替代一些纯粹表现的javascript代码而实现动画,可以通过keyframe显式控制当前帧的属性值。

> animation-fill-mode，这个属性标示是以(from/0%)指定的样式 还是以(to/100%)指定的样式为动画完成之后的样式。这个很方便我们控制动画的结尾样式，保证动画的整体连贯。

## 对 line-height 的理解？

line-height指的是一行字的高度，包含了字间距，实际上是下一行基线到上一行基线的距离。

如果一个标签没有定义height属性(包括百分比高度)，那么其最终表现的高度一定是由line-height起作用

换种理解方式，如果一个有文字的div，不设置高度，并将其行高设置0，div将不会被撑开。

```html
<div class="container">
  <div class="ele">
    this is inner text
  </div>
  <div class="ele1">
    this is inner text
  </div>
</div>
复制代码
.container{
    width: 220px;
    height:100px;
    border: 1px solid grey;
}
div{
   margin-top: 20px;
   border: 1px solid grey;
}
.ele{
 line-height:0;
}
复制代码
```

​    this is inner text  

​    this is inner text  

详情可移步[可食用的「css布局干货」,纯Html示例，可调试 | 水平、垂直、多列](https://juejin.im/post/6844904164435181581#heading-9) 中`line-height` 部分

## CSS 外边距(margin)重叠及防止方法

相邻的两个盒子（可能是兄弟关系也可能是祖先关系）的外边距可以结合成一个单独的外边距。 这种合并外边距的方式被称为折叠，结合而成的外边距称为折叠外边距。

折叠结果遵循下列计算原则：

两个相邻的外面边距是正数时，折叠结果就是他们之中的较大值； 两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大值； 两个外边距一正一负时，折叠结果是两者的相加的和；

什么情况下不会产生外边距重叠？

1. 水平边距永远不会重合。
2. 相邻的盒模型中，如果其中的一个是浮动的（float），垂直margin不会重叠，并且浮动的盒模型和它的子元素之间也是这样。
3. 设置了overflow属性的元素和它的子元素之间的margin不被重叠（overflow取值为visible除外）。
4. 设置了绝对定位（position:absolute）的盒模型，垂直margin不会被重叠，并且和他们的子元素之间也是一样。

其实边距重叠主要是由于重叠的两个元素处于同一个BFC下。通过某些属性使元素生成新的BFC上下文即可解决

### 什么是BFC？怎么触发BFC？有什么用？

BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

#### BFC的布局约束规则

- 内部的Box会在垂直方向，一个接一个地放置。
- Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。
- 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。即BFC中子元素不会超出他的包含块。
- BFC的区域不会与float box重叠。
- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
- 计算BFC的高度时，浮动元素也参与计算。

#### BFC触发方式

1. 根元素，即HTML标签
2. 浮动元素：float值为left、right
3. overflow值不为 visible，为 auto、scroll、hidden
4. display值为 inline-block、table-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid
5. 定位元素：position值为 absolute、fixed **注意：** `display: table`也可以生成BFC的原因在于Table会默认生成一个匿名的table-cell，是这个匿名的table-cell生成了BFC。

### BFC作用

BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然。我们可以利用BFC的这个特性来做很多事。

1. 同一个 BFC 下外边距会发生折叠
2. BFC 可以包含浮动的元素（清除浮动
3. BFC 可以阻止元素被浮动元素覆盖

[BFC示例及详细讲解](https://juejin.im/post/6844904200900460558)

## display: none; 与 visibility: hidden; 有什么区别？

两者都会使元素变得不可见。

| 区别     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| 文档流   | display: none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见； |
| 继承性   | display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility:hidden;是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式； |
| 渲染影响 | 修改元素的display属性使元素消失或显示通常会造成回流。修改visibility属性只会导致重绘 |
| 读屏器   | 无法读取 `display: none`的元素内容；会读取visibility: hidden元素内容； |

## 隐藏元素的方法有哪几种？

- `visibility: hidden`: 隐藏某个元素，但是元素占用的空间任然存在；
- `opacity: 0`: 使一个元素完全透明；
- `position: absolute + 一个很大的 left 负值定位`: 使元素定位在可见区域之外；
- `display: none`:  元素不可见，并且不再占用文档的空间；
- `transform: scale(0)`:  将一个元素设置为缩放无限小，元素将不可见，元素原来所在的位置将被保留；
- `<div hidden="hidden">`:  HTML5属性,效果和display:none;相同，但这个属性用于记录一个元素的状态；
- `height: 0`:  将元素高度设为 0 ，并消除边框，有时需同步设置`overflow: hidden`；
- `filter: blur(0)`:  CSS3属性，括号内的数值越大，图像高斯模糊的程度越大，到达一定程度可使图像消失;

## li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

浏览器的默认行为是把inline元素间的空白字符（空格换行tab）渲染成一个空格。换行后会产生换行字符，而它会变成一个空格，当然空格就占用一个字符的宽度。

解决办法：

1. 将< li>代码全部写在一排
2. 将`ul`字符尺寸直接设为0，重设`li`的字符尺寸
3. 将`ul`的字符间隔设置为-5px，重设`li`的字符尺寸

```css
.wrap ul{letter-spacing: -5px;}
.wrap ul li{letter-spacing: normal;}
复制代码
```

1. 设置`li`的属性`float：left`；

虽然我很久没纯手写ul了。。。

## JS如何获取盒模型的位置及宽高

1. dom.style.width/height 这种方法只能获取到内联样式的宽和高，而样式一般不回以内联方式写，所以这种方式不适用现在大多数的开发；
2. window.getComputedStyle(dom).width/height getComputedStyle()是一个可以获取当前元素所有**最终**使用的CSS属性值的方法；兼容性很好。
3. dom.getBoundingClientRect() getBoundingClientRect用于获取某个元素相对于视窗的位置集合。集合中有top, right, bottom, left,height,width,x,y共8个属性

```
const rectObject = dom.getBoundingClientRect()
复制代码
```

- rectObject.top：元素上边到视窗上边的距离;
- rectObject.right：元素右边到视窗左边的距离;
- rectObject.bottom：元素下边到视窗上边的距离;
- rectObject.left：元素左边到视窗左边的距离;
- rectObject.width：元素宽度;
- rectObject.height：元素高度;
- rectObject.x：元素内容与视口的水平距离;
- rectObject.y：元素内容与视口的垂直距离;

## 怎么让Chrome支持小于12px 的文字

针对谷歌浏览器内核，加webkit前缀，用transform:scale()这个属性进行缩放！

```css
.text {
    -webkit-transform: scale(0.8);
}
复制代码
```

## 浏览器如何判断元素是否匹配某个CSS选择器

浏览器先产生一个元素集合，这个集合往往由最后一个部分的索引产生（如果没有索引就是所有元素的集合）。然后向上匹配，如果不符合上一个部分，就把元素从集合中删除，直到真个选择器都匹配完，还在集合中的元素就匹配这个选择器了。

举个例子，有选择器： `body.ready #wrapper > .lol233`

先把所有 class 中有 lol233 的元素拿出来组成一个集合，然后上一层，对每一个集合中的元素，如果元素的 parent id 不为 #wrapper 则把元素从集合中删去。 再向上，从这个元素的父元素开始向上找，没有找到一个 tagName 为 body 且 class 中有 ready 的元素，就把原来的元素从集合中删去。

至此这个选择器匹配结束，所有还在集合中的元素满足。

之所以从后往前匹配因为效率和文档流的解析方向。效率不必说，找元素的父亲和之前的兄弟比遍历所有儿子快而且方便。

关于文档流的解析方向，是因为现在的 CSS，一个元素只要确定了这个元素在文档流之前出现过的所有元素，就能确定他的匹配情况。应用在即使 html 没有载入完成，浏览器也能根据已经载入的这一部分信息完全确定出现过的元素的属性。

为什么是用集合主要也还是效率。基于 CSS Rule 数量远远小于元素数量的假设和索引的运用，遍历每一条 CSS Rule 通过集合筛选，比遍历每一个元素再遍历每一条 Rule 匹配要快得多。

## 移动端如何实现1px

同样是1px，移动端的1px 就会显得很粗。

> 在早先的移动设备中，屏幕像素密度都比较低，如iphone3，它的分辨率为320x480，在iphone3上，一个css像素确实是等于一个屏幕物理像素的。后来随着技术的发展，移动设备的屏幕像素密度越来越高，从iphone4开始，苹果公司便推出了所谓的Retina屏，分辨率提高了一倍，变成640x960，但屏幕尺寸却没变化，这就意味着同样大小的屏幕上，像素却多了一倍，这时，一个css像素是等于两个物理像素的。

方案1: 0.5px
 通过 JavaScript 检测浏览器能否处理0.5px的边框，如果可以，给元素添加个class。

方案2: 使用图片实现 生成一张边缘透明的图片，以重叠方式展示`border-image: url(border.gif) 2 repeat;`

方案3: 多背景渐变实现
 设置1px的渐变背景，50%有颜色，50%透明，但是无法实现圆角

方案4: 伪类 + transform 把原先元素的 border 去掉，然后利用 :before 或者 :after 重做 border ，并 transform 的 scale 缩小一半。原先的元素相对定位，新做的 border 绝对定位

方案5(推荐)：通过 viewport + rem 实现

```css
var viewport = document.querySelector("meta[name=viewport]");

//下面是根据设备像素设置viewport
if (window.devicePixelRatio == 1) {
  viewport.setAttribute('content', 'width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no');
}
if (window.devicePixelRatio == 2) {
  viewport.setAttribute('content', 'width=device-width,initial-scale=0.5, maximum-scale=0.5, minimum-scale=0.5, user-scalable=no');
}
if (window.devicePixelRatio == 3) {
  viewport.setAttribute('content', 'width=device-width,initial-scale=0.3333333333333333, maximum-scale=0.3333333333333333, minimum-scale=0.3333333333333333, user-scalable=no');
}

// 设置对应viewport的rem基准值
var docEl = document.documentElement;
var fontsize = 16* (docEl.clientWidth / 375) + 'px';
docEl.style.fontSize = fontsize;
复制代码
```

此处不再详细赘述。五种方案的具体实现及详细讲解请移步【[viewport和1px | 工具人: 这是1px，设计师： 不，这不是](https://juejin.im/post/6844904163160096782)】

## CSS有哪些属性是可以继承的？

1、字体系列属性

- font-family：字体系列
- font-weight：字体的粗细
- font-size：字体的大小
- font-style：字体的风格

2、文本系列属性

- text-indent：文本缩进
- text-align：文本水平对齐
- line-height：行高 -word-spacing：单词之间的间距
- letter-spacing：中文或者字母之间的间距
- text-transform：控制文本大小写（就是uppercase、lowercase、capitalize这三个）
- color：文本颜色

3、元素可见性：

- visibility：控制元素显示隐藏

4、列表布局属性：

- list-style：列表风格，包括list-style-type、list-style-image等

5、光标属性： - cursor：光标显示为何种形态

## React Native中的css样式？

React Native 的样式基本上是实现了 CSS 的一个子集，这些样式名基本上是遵循了 web 上的 CSS的命名，只是按照 JS 的语法要求使用了驼峰命名法。

1.内联样式： 一般情况下，内联样式简单粗暴，让你可以快速的调试，

```
<Text style = {{fontSize:20,fontStyle:'normal',fontWeight:'bold'}}>测试</Text>
复制代码
```

2.对象样式： 对比内联样式的语法，是将内联样式分离出来，避免每一次render方法时都进行创建样式

```
 const italic = {fontSize:20, fontStyle:'italic',fontWeight:'bold'};
 <Text style = {italic}>我是对象样式</Text>
复制代码
```

3.使用StyleSheet.create：
 StyleSheet.create创建的样式，可以减少内存分配数，从而提高性能，StyleSheet是不可变的，通常能够带来一些遍历，

StyleSheet还能帮你检查样式语法是否合理。所以它是一个不错的样式选择

```
const styles = StyleSheet.create({font:{fontSize:20,fontStyle:'italic',fontWeight:'bold'},content:{backgroundColor:'#aaaaaa'}});
<Text style ={styles.font}>我是StyleSheet.create创建的样式</Text>
复制代码
```

4.样式拼接： 一个组件对多个样式的复用，就可以使用样式拼接，样式拼接是结合样式的一种实用的方法

```
    const styles = StyleSheet.create({font:            {fontSize:20,fontStyle:'italic',fontWeight:'bold'},content:{backgroundColor:'#aaaaaa'}});
    <Text style = {[styles.content,styles.font]}>我是组合样式一</Text>
    <Text style = {[styles.content,styles.font,{color:'#666666'}]}>我是组合样式二</Text>
复制代码
```

1. 条件样式： 根据渲染逻辑对组件进行样式设置

```
 <Text style = {this.state.toucher && styles.font}>我是条件样式</Text>
复制代码
```

1. 使用父类样式 使用组件样式进行传递，从而更有效的被父组件控制流程和操作样式。

```
 <Text style = {this.props.style}>我是父类的属性样式</Text>
复制代码
```

RN使用 JavaScript 来写样式，所有核心组件都接受名为style的属性，只要最终结果的类型是正确的，你可以使用任何js语法来生成style对象

> 在 React Native中默认使用 Flexbox 规则来指定某个组件的子元素的布局。

## style标签写在body后与body前有什么区别

style元素出现在body元素，最终效果和style元素出现在head里是一样的。

页面加载是自上而下的。将style标签放于body之前，为的是先加载样式。若是写在body标签之后，由于浏览器以逐行方式对html文档进行解析，当解析到写在文档中的样式表时，会导致浏览器停止之前的渲染，等待加载且解析样式表，可能引起FOUC、重绘或重新布局

根据当前标准，<link rel=stylesheet …> 是可以出现在body元素中的。并且也可能引起上述问题。然而link是引用资源，意味着可以用于故意设计的异步加载。而style元素是直接内嵌的，并没有合理的use case去使用它。所以html标准中允许body中出现link，而不允许style。

## position:fixed;在手机端下无效怎么处理？

fixed 定位其实是相对与浏览器视口来定位的。移动浏览器有两个视口：可视视口和布局视口。

当在屏幕上滑动时是在滑动整个viewport，那么原来的网页还在，fixed也没有变过位置，但是相对于可视视口，fix元素就移动了位置。

如果是水平方向上的固定，可以通过

```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
复制代码
```

来设置网页宽度等于屏幕宽度，并且不允许用户缩放，当然，设计上就需要适配了

另一种是垂直方向上的问题。 iOS 下经常会有 fixed 元素和输入框(input 元素)同时存在的情况。例如，页面底部有fix页脚， 但是 fixed 元素在有软键盘唤起的情况下，会出现许多莫名其妙的问题。比如页面没变化，只有fix元素发生位置变化，破坏了整体布局。

这也是可视视口和布局视口高度不一致的问题，调整页面布局，将body高度设成手机屏幕高度，即页面整体不滚动，滚动区域包裹在子组件中，并自适应高度，这样最外层的fix元素在被键盘顶起的时候，页面也会随之变化，相当于浏览器高度发生了变化。

## 什么是回流（重排）和重绘以及其区别

回流与重绘，会影响页面性能，每次这两个都会被同时提及，关系就好像KFC边上一定会有MC一样亲密的让人摸不到头脑。

在页面加载时，浏览器渲染过程如下：

1. 解析HTML，生成DOM树，解析CSS，生成CSSOM树
2. 将DOM树和CSSOM树结合，生成渲染树(Render Tree)
3. Layout(回流):根据生成的渲染树，进行回流(Layout)，得到节点的几何信息（位置，大小）
4. Painting(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素
5. Display:将像素发送给GPU，展示在页面上。（这一步其实还有很多内容，比如会在GPU将多个合成层合并为同一个层，并展示在页面中。而css3硬件加速的原理则是新建合成层）

**回流**

通过构造渲染树，将可见DOM节点以及它对应的样式结合起来，这时候需要计算它们在设备视口(viewport)内的确切位置和大小，这个计算的阶段就是回流。每个页面至少需要一次回流，就是在页面第一次加载的时候，这时候是一定会发生回流的，因为要构建render tree。

**重绘**

通过构造渲染树和回流阶段，我们确定了可见节点，以及可见节点的样式和具体的几何信息(位置、大小)，将渲染树的每个节点都转换为屏幕上的实际像素，这个阶段就叫做重绘节点。

**会导致回流的操作：**

- 页面首次渲染
- 浏览器窗口大小发生改变
- 元素尺寸或位置发生改变（包括外边距、内边框、边框大小、高度和宽度等）
- 元素内容变化（文字数量或图片大小，比如用户在input框中输入文字等等）
- 元素字体大小变化
- 添加或者删除**可见**的`DOM`元素
- 激活`CSS`伪类（例如：`:hover）`
- 查询某些属性或调用某些方法

## 行内元素和块级元素的具体区别是什么？行内元素的 padding 和 margin 可设置吗？

**块级元素( block )特性：**

总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示；

宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制；

**内联元素(inline)特性：**

和相邻的内联元素在同一行;

宽度(width)、高度(height)、内边距的top/bottom和外边距的top/bottom都不可改变（也就是padding和margin的left和right是可以设置的）。

浏览器还有默认的天生inline-block元素（拥有内在尺寸，可设置高宽，但不会自动换行）
 `<input> 、<img> 、<button> 、<textarea>。`

## img 图片自带边距的问题是什么原因引起的？如何解决？

图片底部的空隙实际上涉及行内元素的布局模型，图片默认的垂直对齐方式是基线，而基线的位置是与字体相关的。所以在某些时候，图片底部的空隙可能是 2px，而有时可能是 4px 或更多。不同的 font-size 应该也会影响到这个空隙的大小。

1. 转化成（行级）块元素

```
 display : block
复制代码
```

1. 浮动，浮动后的元素默认可以转化为块元素（可以随意设置宽高属性）

```
float ： left；
复制代码
```

1. 给 img 定义 vertical-align（消除底部边距）

```
img{    
    border: 0;    
    vertical-align: bottom;
}
复制代码
```

1. 将其父容器的font-size 设为 0；
2. 给父标签设置与图片相同的高度

## 说说css层叠上下文

大部分人在初步学完css后，对z-index的印象大概处于“`z-index`就是用来描述定义一个元素在屏幕`Z轴`上的堆叠顺序”。例如，如果A元素和B元素重叠了，这么说有点枯燥，换个说法，

1. 如果漂亮妹子A和文字B注释重叠了
2. 但是页面渲染的时候，文字处于图片之上，挡住你看妹子了
3. 这时候，你可能会
   - 设置妹子的z-index为999
   - 设置文字的z-index为-1

就是这么差别对待。既然拿上面那一段举栗子，那就代表这种理解有问题，至少是不严谨的。

1. `z-index`属性仅在**定位元素**（定义了[position](https://juejin.im/post/6844904159292948493)属性，且属性值为非`static`值的元素）上有效果。
2. 元素在`Z轴`上的堆叠顺序，由元素所属的**层叠上下文**、元素的**层叠水平**、以及元素在**文档中的顺序**等共同决定，元素的`z-index`值的只是决定元素的层叠水平的条件之一。

**什么是“层叠上下文”**

层叠上下文(stacking context)，是HTML中一个三维的概念。它划分了某种领域或范围，在渲染规则层面，将内部与外部隔开，并赋予元素自身及内部区域某些特性。

在CSS2.1规范中，每个盒模型的位置是三维的，即元素除了在页面上沿`X轴Y轴`平铺，同时还拥有一个相对屏幕垂直的纵深，也就是表示层叠的`Z轴`。

**如何创建“层叠上下文”** 层叠上下文大部分由一些特定的CSS属性创建。

- HTML中的根元素本身就具有层叠上下文，称为“根层叠上下文”。
- 普通元素设置position属性为非static值并设置z-index属性为具体数值，产生层叠上下文。 css3补充了一些创建层叠上下文的条件，后面会列举。

**层叠顺序**

层叠顺序(stacking order)， 表示元素发生层叠时的特定的垂直显示顺序，是一种用于确定元素层叠水平的规则。

当元素重叠时，必须决定哪部分内容展示在屏幕上，因此，层叠顺序决定了一条优先级规则，也可以称为等级链规则。 以下排名分先后，自上而下优先级越来越低：

1. z-index > 0 (要求z-index属性生效)
2. z-index: auto 或者 z-index: 0 (z-index: auto 不会创建层叠上下文)
3. inline、inline-block 行内盒子
4. float浮动盒子
5. block块级盒子，非 inline-block，无 position 定位（static除外）的子元素
6. z-index < 0
7. 层叠上下文元素的 `background/border`

当元素发生层叠的时候，其覆盖关系通常遵循下面2个准则：

1. 在同一个层叠上下文领域，当具有明显的层叠水平标示的时候，如有效的 `z-index` 值，层叠水平值大的那一个覆盖小的那一个。
2. 当元素的层叠水平一致、层叠顺序相同的时候，在DOM流中处于后面的元素会覆盖前面的元素。

具体讲解及案例分析请移步[前端必须掌握的「CSS层叠上下文」讲解](https://juejin.im/post/6844904168382005261)

## css百分比单位相对基准

对于包含在父元素中的子元素，padding、margin等设为百分比或负值时，并不是上下边距相对于父元素高度，左右边距相对于父元素宽度。

1. width height 百分比

当元素的height、width设置为百分比时，分别基于包含它的块级对象的高度、宽度。这个是常规百分比的含义。

1. margin 百分比 `margin` 的百分比值参照其包含块的宽度进行计算。当书写模式变成纵向的时候，其参照将会变成包含块的高度。 **为什么**

> CSS权威指南中的解释：
>
> 我们认为，正常流中的大多数元素都会足够高以包含其后代元素（包括外边距），如果一个元素的上下外边距是父元素的height的百分数，就可能导致一个无限循环，父元素的height会增加，以适应后代元素上下外边距的增加，而相应的，上下外边距因为父元素height的增加也会增加。

1. padding 百分比 同上
2. width、padding 联合百分比 在标准盒模型下，` width: 100%; padding: 10% 10%;` 会导致内部元素溢出，如果遇到这种情况，一般都会使用怪异盒模型，即设置`box-sizing: border-box`，这时候`width`的值是会包含`padding`的距离的。
3. translate百分比 在translate 函数当中使用百分比是以该元素自身的宽高作为基准。
4. margin为负值
   1. margin-left,margin-right为负值
      - 元素本身没有宽度，会增加元素宽度
      - 元素本身有宽度，会产生位移
   2. margin-top为负值，不管是否设置高度，都不会增加高度，而是会产生向上的位移
   3. margin-bottom为负值的时候不会位移,而是会减少自身供css读取的高度.
5. padding 为负值 很遗憾，padding不允许指定为负，指定了也无效～


作者：碎_浪
链接：https://juejin.cn/post/6854573221291753480
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。