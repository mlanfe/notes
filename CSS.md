### 元素框

1.margin, width, height可以设为auto; padding不可以设为auto; 只有margin可以为负值

2.块级元素的width+padding+margin = 块级元素的父元素的width



### 浮动



3.其他元素围绕着浮动元素排列

4.多个浮动元素在父级容纳块中会自动换行

5.浮动的规则: 浮动元素不会折叠





**BFC**: BFC就是页面上的一个隔离的独立容器，容器`里面`的子元素不会影响到外面的元素。

**BFC的布局约束规则**

1. 内部的Box会在垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。
3. 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。即BFC中子元素不会超出他的包含块。
4. 计算BFC的高度时，浮动元素也参与计算。BFC的区域不会与float box重叠。
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

**开启BFC**

1. overfolw:hidden(推荐)/auto/scroll

2. float浮动的值不为none(导致元素的宽度丢失)
3. display的值为table-cell/table-caption/inline-block
4. position的值不为static或releative

**外边距折叠与BFC**

1. 只有块级元素才会发生外边距的折叠, inline-block元素的外边距不会发生折叠

2. 在一个BFC中的相邻块级元素会发生外边距重叠，解决办法：	

- 转变其中一个元素为inline-block
- 给其中一个元素添加父元素并设置`overflow:hidden`开启BFC
- 在相邻块级元素间添加一个br以分割开2个元素

3. 在一个BFC中父子元素会发生外边距传递，导致重叠，解决办法：

- 给父元素设置`overflow:hidden`,开启BFC
- 给父元素设置内边距，避免外边距传递的发生
- 给父元素加边框，阻隔传递

**浮动与BFC**

元素加了浮动后，会脱离文档流，提升了半层层级，向着指定方向移动，直到遇到父元素的边界或另一个浮动元素停止。也就是说，没有触发BFC的元素的元素，其下半层会被浮动元素覆盖，上半层会被浮动元素往后推。`层级`：如果将整个元素看做一层，则下半层是元素本身（背景样式等），上半层是元素中的内容

浮动: 导致的父元素高度坍塌;影响兄弟元素的位置

清除浮动: 触发父元素的BFC;在最后一个浮动元素后添加一个兄弟元素,并添加clear:both样式

**百分比相对基准**

height、width、top、left、right、bottom:参照其包含块的高度、宽度

padding、margin :参照其包含块的宽度

translate：参照其自身的宽高

**margin为负值**

除了块元素未设置宽度会增加宽度外，其他的几种情况都是反向移动或者减少css读取的值







 