# Flex布局
Flex意为“弹性布局”，用来为盒模型提供最大的灵活性，任何一个容器都可以指定为Flex布局(行内元素也可以使用Flex布局),webkit内核的浏览器，必须加上`-webkit`前缀

**设为Flex布局以后，子元素的float、clear、vertical-align属性将实效**

## 基本概念

采用Flex布局的元素，成为Flex容器，简称“容器”。它的所有子元素自动成为容器成员，称为Flex项目，简称”项目“

容器默认存在两根轴，水平的主轴(main axis)和垂直的交叉轴(cross axis)，main start,main end, cross start, cross end

## 容器的属性

以下6个属性设置在容器上

* flex-direction 
* flex-wrap  
* flex-flow
* justify-content
* align-items
* align-content

### flex-direction 决定主轴的方向
* row 水平方向 左端开始
* row-reverse 水平 右端开始
* column 竖直方向 上端开始
* column-reverse 竖直方向 下端开始

### flex-wrap 一条轴线排不下，如何换行
* nowrap 不换行
* wrap 第一行在上方
* wrap-reverse 第一行在下方

### flex-flow 是flex-direction和flex-wrap属性的简写

### justify-content 定义了项目在主轴上的对齐方式,与主轴的方向有关系，假设是从左到右

* flex-start default 左对齐
* flex-end 右对齐
* center 居中
* space-between 两端对齐，项目之间的间隔都相等
* space-around 每个项目两侧的间隔相等，所以，项目之间的间隔比项目与边框的间隔大一倍

### align-items 定义项目在交叉轴上如何对齐，与交叉轴的方向有关，假设交叉轴的方向为从上到下

* flex-start 交叉轴的起点对齐
* flex-end 交叉轴的终点对齐
* center 交叉轴的中点对齐
* baseline 项目的第一行文字的基线对齐
* stretch default 如果项目未设置高度或设为auto，将占满整个容器的高度

### align-content 定义了多根轴线的对齐方式，如果项目只有一根轴线，该属性不起作用

* flex-start 与交叉轴的起点对齐
* flex-end 与交叉轴的终点对齐
* center 与交叉轴的中点对齐
* space-between 与交叉轴两端对齐，轴线直线的间隔比轴线与边框的间隔大一倍
* space-around 每根轴线两侧的间隔都相等，所以，轴线之间的间隔比轴线与边框的间隔大一倍
* stretch default 轴线占满整个交叉轴

## 项目的属性
* order
* flex-grow
* flex-shrink
* flex-basis
* flex
* align-self

* order 定义项目的排列顺序。数值越小，排列越靠前 default 0
*  flex-grow 属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大，如果所有的项目的`flex-grow`属性都为1，则它们将等分剩余空间(如果有的话).如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍
*  flex-shrink 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小，如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小，如果一个项目的flex-shrink为0，其他为1，则空间不足时，前者不缩小
*  flex-basis 定义了在分配多余空间之前，项目占据的主轴空间，浏览器根据这个属性，计算主轴是否有多余空间。默认为auto，即项目的本来大小
*  flex 是flex-grow,flex-shrink,flex-basis,默认值为0 1 auto
*  align-self 允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性

