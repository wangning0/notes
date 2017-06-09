# CSS Review
* web字体的基本思想：链接字体文件，让网页可以使用任何字体，即使网站访客的电脑中没有安装你使用的字体也无妨
* 伪元素和伪类

    ```
    为了区别伪元素和伪类，伪元素可以使用双冒号表示，伪类单冒号表示，但是IE8以前不兼容双冒号的写法
    
    伪类：
        :focus
        :link
        :visited
        :hover
        :active
        :first-child
        :last-child
        :only-child
        :nth-child()
        :target
        :not()
    伪元素：
        first-line
        first-letter
        before
        after
        ::selection 鼠标按下后拖动的选择 css3(只能设置color和background-color)
    ```
* + 表示紧邻的兄弟元素， ～ 表示所有的兄弟元素
* 继承

    ```
    继承是指，应用在某个标签上的css属性传给了内部嵌套的标签，css属性也能隔代继承

    不能继承的属性：
        display、margin、border、padding、background、height、min-height、max- height、width、min-width、max-width、overflow、position、left、right、top、 bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、 page-bread-before和unicode-bidi
    能继承的属性：
        所有元素可继承：visibility和cursor。
        内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、 font-family、font-size、font-style、font-variant、font-weight、text- decoration、text-transform、direction。
        块状元素可继承：text-indent和text-align。
        列表元素可继承：list-style、list-style-type、list-style-position、list-style-image。
        表格元素可继承：border-collapse。
    ```

* 层叠

    ```
    层叠是用于管控样式之间相互作用的方式，出现冲突时判断哪个样式的优先级高
    
    层叠规则：
        最近的祖辈胜出
        直接应用在标签上的样式胜出
        特指度
            一个标签选择符记 1分
            一个类选择符记 10分
            一个ID选择符记 100分
            一个行内样式记 1000分
    ```

## CSS 实战技术

* 使用web字体

    ```
    所有主流浏览器都支持Web字体，使用Web字体时，浏览器会从Web服务器中下载字体，然后显示网页中的字体
    
    css中设定web字体的方式：
        1. @font-face指令，负责告诉浏览器字体的名称和下载地址
        2. font-family属性，指定web字体的方式与指定电脑中已安装字体的方式一样

    字体文件的类型
        1. EOT（嵌入式OpenType）,只有IE支持这种字体
        2. TrueType和OpenType，电脑中的.ttf .otf格式的字体，电脑字体最常使用这两种格式。这两种字体格式可以在文字处理软件和桌面出版软件里使用，也可以在网页中使用
        3. WOFF，Web开放字体格式时专为web设计的，基本上算是TrueType或OpenType格式的压缩版，因此文件体积通常较小，比其他字体格式下载得快
    ```
    * 为文本着色
    
        ```
        RGB
            红 绿 蓝
        RGBA    IE8以前的版本不兼容
            红 绿 蓝 透明度
        HSL
            eg: color: hsl(0. 100%, 50%);
            第一个参数是角度，取值范围是0-360,对应于色圆
            第二个参数是饱和度，即颜色的纯度
            第三个参数是亮度
        ```
    
    * 修改字号

        ```
        px 
        关键字
            xx-small x-small small
            medium large x-large xx-large
        百分比
            相对于父元素字体的大小
        em
            和百分比的原理相似
        rem
            字号的大小根据根元素来决定
        ```
        
        * 装饰词语和字符
        
            ```
            font-style
            font-weight
                100-900 
            text-transform
                uppercase 大写
                lowercase 小写
                capitalize 首字母变成大写
            text-decoration
                underline
                overline
                line-through
                blink
            text-shadow
                1. 横向偏移值
                2. 纵向偏移值
                3. 阴影的模糊程度
                4. 投影的颜色
            ```
        * 装饰整个段
        
            ```
            line-height
                使用%/em 可以使行间距会随着font-size属性的值按比例变化
                默认的line-height: 120%;
                使用数字设定行间距
                    line-height: 1.5;
                    遇到这种值时，浏览器会拿它乘以字号，确定行高是多少，然而由于嵌套的标签会从父辈标签继承line-height属性的值，如果使用em／%为单位设定行间距，会遇到问题，因为line-heighth会继承，而且继承的不是百分数，而是计算得到的具体行高
            
            text-align
            text-indent 首行缩进
            ```
            
        * 装饰列表el
        
            ```
            list-style-type
            list-style-position
            list-style-image
            ```
            
        * 外边距冲突

            ```
            解决办法：
                1. 设定一些内边距
                2. 添加边框，因为两个外边距之间有边框或内边距，因此不再相连。
                
            把外边距设为负值，去掉空白
            ```
            
        * 投影

            ```
            box-shadow
                第一个参数： 横向偏移
                第二个参数： 纵向偏移
                第三个参数： 投影的半径
                第四个参数： 投影的颜色
             投影会强制浏览器多次重新渲染和重新绘制，所以要慎重选择
            ```
        * 浮动对背景和边框的影响
            
            ```
            web浏览器只会让文字围绕浮动的元素显示，而不包括边框或者背景，解决办法
                1. 为浮动元素下面设置了背景或边框的元素添加一个样式规则，找到样式后，添加这一行代码:overflow: hidden
                2. 在浮动元素的四周添加边框线，如果边框线足够宽，而且颜色于页面的背景色一样，边框看起来就像是空白的
            ```     
        
        * clear 不要围着浮动的元素显示
            
            ```
            left 让元素显示在左浮动的元素下面，不过仍然围着右浮动的元素
            right 让元素显示在右浮动的元素下面，不过仍然围着左浮动的元素
            both 强制让元素显示在左浮动和右浮动的元素下面
            ```
* 背景图
    
    ```
    background-attachment
        scroll 背景图与文本和页面中的其他内容一起滚动
        fixed  把背景图固定在某个位置
    background-origin 重新定义图像的起点
        border-box: 从边框的左上角开始放置背景图
        padding-box: 从内边距的左上角开始放置背景图
        content-box: 从内容区域的左上角开始放置
    background-size
        contain 根据元素的背景尺寸强制调整图像的尺寸
        cover 强制让图像的宽度适应元素的宽度，让图像的高度适应元素的高度，而且不破坏图像的纵横比
    background-image: url(...) center top no-repeat,
                      url(...) center center no-repeat,
                      url(...) center bottom no-repeat
                      
    ```   
* CSS 变形，过渡和动画
 
    ```
    transform 使用这个属性时要指定变形的类型以及表示变形程度的值
        rotate(deg) 顺时针旋转
        scale(n) 放大n倍 负数则翻转
        translate(x, y) 平移
        skew(deg, deg) 倾斜
        translateZ(0) 表示用GPU加载
    transform-origin 修改变形原点
    
    过渡满足的条件
        两个样式
        transition属性
            transition-property 指定要以动画方式变化的属性(所有属性则用all)
            transition-duration 指定动画持续时间长度
        触发器
            transition-tinming-function 动画的速率
                linear
                ease
                ease-in
                ease-out
                ease-in-out
            transition-delay 延迟动画的加载
            
    动画
        css过渡只能把一系列CSS属性葱一个状态变到另外一个状态，css动画则能把一系列CSS属性从一个状态变到另一个状态。再变到第三个状态还可以继续变化，还可以重播动画，暂停动画，倒播动画
        
        创建动画两步
            1. 定义动画， 设置关键帧，列出要变化的css属性
            2. 把动画应用到元素上
        
        @keyframse animationName {
            from {
                // ...
            }
            to {
                // ...
            }
        }
        
        .className {
            animation-name: animationName;
            animation-duration: time;
        }
         
         animation-timing-function  控制整个动画的播放速率
         animation-iteration-count 播放次数
         animation-direction 播放的方向
         animation-play-state running paused
    ``` 
    
* 浮动的问题
    
        ```
        解决方案
            1. 在外层元素的底部添加一个元素，清除浮动
            2. 浮动外层元素
            3. 使用overflow: hidden   
            4. :after {
                    content: " "
                }
        ```

* 如何让分栏看起来等高
        
        ```
        https://css-tricks.com/fluid-width-equal-height-columns/
        ```
 * 响应式Web布局
 
    ```
    三大理念：
        1. 使用弹性栅格布局
        2. 使用弹性媒体显示图像和视频
        3. 使用css媒体查询为不同宽度的屏幕编写不同的样式
    ``` 
* 使用CSS栅格系统
    
    ```
    在Web设计领域，栅格是一种把内容组织到行和列中的方式，而且各列的宽度是一致的。先把页面的整个宽度分成一系列"单元"，然后自由组合单元，形成不同宽度的分栏，常用的单元数是12，因为12可以整除2 3 4
    大多数css栅格系统都使用百分比值定义单元的宽度
    ```
## Flex布局

Flex意为“弹性布局”，用来为盒模型提供最大的灵活性，任何一个容器都可以指定为Flex布局(行内元素也可以使用Flex布局),webkit内核的浏览器，必须加上-webkit前缀

**设为Flex布局以后，子元素的float、clear、vertical-align属性将实效**
form

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

## CSS居中的方式
[居中方式](https://zhuanlan.zhihu.com/p/25068655?refer=learncoding)

[居中方式](http://elevenbeans.github.io/2016/05/04/css-%E4%B8%AD%E7%9A%84%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD%E6%B3%95/)

### 水平居中

**已知宽度**

* 水平居中的margin: 0 auto;
    
    ```
        <style>
          * {
            padding: 0px;
            margin: 0px;
          }
           .parent {
              width: 500px;
              height: 500px;
              border: 1px solid black;
           }
           .child {
             width: 100px;
             height: 100px;
             margin: 0 auto;
             background: red;
           }
        </style>
    </head>
    <body>
     <div class="parent">
       <div class="child"></div>
     </div>
    </body>
    ```
    
* 水平居中text-align: center(内联元素)

    ```
        <style>
          * {
            padding: 0px;
            margin: 0px;
          }
           .parent {
              width: 500px;
              height: 500px;
              border: 1px solid black;
              text-align: center;
           }
           .child {
             display: inline-block;
             width: 100px;
             height: 100px;
             background: red;
           }
        </style>
    </head>
    <body>
     <div class="parent">
       <div class="child"></div>
     </div>
    ```
### 水平垂直居中

**已知高度**

* 定位和需要定位的元素的margin减去宽高的一半

    ```
    <style>
      * {
            padding: 0px;
            margin: 0px;
          }
           .parent {
              width: 500px;
              height: 500px;
              border: 1px solid black;
              text-align: center;
              position: relative;
           }
           .child {
             display: block;
             width: 100px;
             height: 100px;
             background: red;
             position: absolute;
             left: 50%;
             top: 50%;
             margin-top: -50px;
             margin-left: -50px;
           }
        </style>
    </head>
    <body>
     <div class="parent">
       <div class="child"></div>
     </div>
    ```
    * display: table-cell

        ```
        // inline
            <style>
              * {
                padding: 0px;
                margin: 0px;
              }
               .parent {
                  width: 500px;
                  height: 500px;
                  border: 1px solid black;
                  display: table-cell;
                    vertical-align: middle;
                    text-align: center;
               }
               .child {
                 display: inline-block;
                 background: red;
                 width: 100px;
                 height: 100px;
               }
            </style>
        </head>
        <body>
         <div class="parent">
           <div class="child" ></div>
         </div>
        </body>
        ```
    
    **未知宽高**
    
    * 定位和margin:auto

        ```
        <style>
          * {
            padding: 0px;
            margin: 0px;
          }
           .parent {
              width: 500px;
              height: 500px;
              border: 1px solid black;
              position: relative;
           }
           .child {
             display: block;
             background: red;
             position: absolute;
             left: 0;
             top: 0;
             right: 0;
             bottom: 0;
             margin: auto;
           }
        </style>
    </head>
    <body>
     <div class="parent">
       <img class="child" src="./t2.png" alt="">
     </div>
    </body>
        ```

    * 绝对定位和transform

        ```
         <style>
          * {
            padding: 0px;
            margin: 0px;
          }
           .parent {
              width: 500px;
              height: 500px;
              border: 1px solid black;
              position: relative;
           }
           .child {
             display: block;
             background: red;
             position: absolute;
             top: 50%;
             left: 50%;
             transform: translate(-50%,-50%);
           }
        </style>
    </head>
    <body>
     <div class="parent">
       <img class="child" src="./t2.png" alt="">
     </div>
    </body>
        ```
     
    * flexBox居中

        ```
        <style>
        .box{
                width: 300px;
                height: 300px;
                background:#e9dfc7; 
                border:1px solid red;
                display: flex;
                justify-content: center;
                align-items:center;
            }
            img{
                width: 150px;
                height: 100px;
            }
    </style>
    <!--html -->
    <body>
        <div class="box" >
            ![](6.jpg)
        </div>
    </body>
        ```
## 区别
1.text-align:center 设置文本或img标签等一些内联对象（或与之类似的元素）的居中。

2.margin:0 auto 设置块元素（或与之类似的元素）的居中。

## vertical-align

只对inline-table有效果


