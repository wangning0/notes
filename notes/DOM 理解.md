# DOM 理解
[DOM](http://blog.jobbole.com/52430/)

> DOM(文档对象模型)是针对HTML，XML文档的一个API，DOM描绘了一个层次化的节点树

## DOM
```
Node---|--Document-------HTMLDocument
       |
       |--characterData---|----Text
       |                  |----Comment
       |--Element------HTMLElement---|--HTMLHeadElement
       |                             |--...
       |                             |--HTMLButtonElement
       |--Attr
```
### Node类型
Javascript的所有节点类型都是继承来自Node类型，因此所有的节点类型都共享着相同的基本属性和方法

* nodeType 属性，表明节点的类型

    *  Node.ELEMENT_NODE(1)
    *  Node.ATTRIBUTE_NODE(2)
    *  Node.TEXT_NODE(3)
    *  Node.DOCUMENT_NODE(9)
* nodeName 如果该Node类型是元素，则为标签名
* nodeValue nodeType==1 则null
* childNodes 保存着一个NodeList对象，类数组对象，用于保存一组有序的节点
* parentNode 指向文档树中的父节点
* previousSibling 上一个兄弟节点 不存在为null
* nextSibling 下一个兄弟节点 不存在为 null
* firstChild 第一个子元素
* lastChild 最后一个子元素
* hasChildNodes() 方法 
* appendChild(node) 末尾添加一个节点
* insertBefore(node，targetNode) 插入节点
* replaceChild(newNode, targetNode) 替换节点

### Document 类型
Javascript 通过Document类型表示文档，在浏览器中document对象是HTMLDocument（继承自Document类型）的实例。

* domain 获取域名，本身或者上一级域名
* referrer 来源页面的URL
* getElementById(idName) 取得元素
* getElementsByTagName(tagName) 返回一个HTMLCollection对象，该对象和NodeList很相似
 
    * namedItem(name)可以返回HTMLCollection对象中name属性的元素
    
* anchors 返回所有带name特性的a元素
* forms 所有的form元素
* images 所有img元素
* links 所有带href的a元素
* write()
* createElement() 创建元素节点
* createTextNode 创建文本节点
* createAttribute() 创建属性节点
* createComment() 创建注释节点

### Element 类型
特征：

* nodeType == 1
* nodeName 值为元素的标签名
* nodeValue null
* parentNode 可能是Document 或 Element

属性和方法：

* tagName 标签名（大写） 
* HTML元素
    所有的HTML元素都是由HTMLElement类型表示，不是直接通过这个类型，也是通过它的子类型来表示。HTMLElement类型直接继承自Element并添加了一些属性
    * id 元素在文档中的唯一标识图
    * title
    * lang
    * className
    * dir 语言的方向
* 取得特性
    * getAttribute()
    * setAttribute()
    * removeAttribute()

### Text类型 
文本节点又Text类型表示，包含的是可以照字面解释的纯文本内容，纯文本中可以包含转义后的HTML字符，但不能包含HTML代码。

特征：
    
* nodeType的值为3
* nodeName的值为“#text”
* nodeValue 节点所包含的文本
* parentNode 是一个Element
* 没有子节点

### Comment 类型
注释在DOM中是通过Comment类型来表示的

* nodeType 的值为8
* nodeName "#comment"
* nodeValue 注释的内容
* parentNode Document 或者是 Element
* 没有子节点

### Attr属性
元素的特性在DOM中以Attr类型来表示

* nodeType == 2
* nodeName 特性的名称
* nodeValue 特性的值
* parentNode null
* HTML 中 无子节点

## 度量

[DOM度量](http://varnull.cn/domzhi-du-liang/)

clientWidth/clientHeight: 带padding不带滚动条的内容区域

css的width包括了滚动条

scrollWidth/scrollHeight: 和clientWidth一样，但是包含了整个可以滚动的区域 

scrollTop/scrollLeft 溢出部分的距离 

offsetWidth/offsetHeight 包含border不包含margin的长度

clientTop/clientLeft top/left的border的长度

offsetParent/offsetLeft/offsetTop: offsetLeft和offsetTop反映了元素相对于它的offsetParent的偏移量。offsetParent是在布局上的父元素。

## 事件处理(IE 与 W3C的标准不同)

* IE5-IE8不支持addEventListener() removeEventListener() 类似的方法为attachEvent() detachEvent()
* DOM 事件的三级模型
    * 0级模型，直接通过onclick写在HTML里面的事件
    * DOM2是通过addEventListener绑定的事件，还有IE下的DOM2事件通过attachEvent()绑定
    * DOM3是一些新的事件(UI事件，焦点，鼠标，滚轮，文本，键盘合成)
* DOM事件模型
    * a) IE所使用的冒泡型事件
    * b）DOM标准定义的冒泡型与捕获型事件
    
    > 冒泡：自下往上
    > 捕获：自上往下
* 标准DOM事件处理模型
    当一个DOM事件被触发的时候，事件已开始从文档的根节点流向目标对象(捕获阶段)，然后在目标对象上被触发(目标阶段)，之后再回溯到文档的根节点（冒泡阶段）
* IE的取消冒泡为cancelBubble,其他的为stopPropagation
* IE的事件对象为window.event,其他的event

## 事件代理
常用的场景
> 事件代理可以让你使用一个事件监听器去监听大量的DOM节点的事件。

## Event对象
type (String) — 事件的名称

target (node) — 事件起源的DOM节点

currentTarget?(node) — 当前回调函数被触发的DOM节点

bubbles (boolean) — 指明这个事件是否是一个冒泡事件（接下来会做解释）

preventDefault(function) — 这个方法将阻止浏览器中用户代理对当前事件的相关默认行为被触发。比如阻止a元素的click事件加载一个新的页面

stopPropagation (function) — 这个方法将阻止当前事件链上后面的元素的回调函数被触发，当前节点上针对此事件的其他回调函数依然会被触发。（我们稍后会详细介绍。）

stopImmediatePropagation (function) — 这个方法将阻止当前事件链上所有的回调函数被触发，也包括当前节点上针对此事件已绑定的其他回调函数。

cancelable (boolean) — 这个变量指明这个事件的默认行为是否可以通过调用event.preventDefault来阻止。也就是说，只有cancelable为true的时候，调用event.preventDefault才能生效。

defaultPrevented (boolean) — 这个状态变量表明当前事件对象的preventDefault方法是否被调用过

isTrusted (boolean) — 如果一个事件是由设备本身（如浏览器）触发的，而不是通过JavaScript模拟合成的，那个这个事件被称为可信任的(trusted)

eventPhase (number) — 这个数字变量表示当前这个事件所处的阶段(phase):none(0), 

timestamp (number) — 事件发生的时间

## DOM扩展

**选择符API**

* querySelector() 方法
* querySelectorAll() 返回一个NodeList
* matchsSelector() 接收css选择符这个参数
* getElementsByClassName() 返回一个NodeList
* classList属性 

    * add      添加某个class属性
    * remove   删除某个class属性
    * contains 是否包含class属性
    * toggle   反转class属性

**HTML5**

兼容模式

`document.compatMode` 属性可以区别渲染页面是标准的还是混杂的，标准模式是：CSS1Compat, 混杂模式是：BackCompat

字符集属性

`document.charset`

自定义数据属性

可以通过元素的dataset属性来访问自定义属性的值，

## 元素大小

**偏移量**

元素的大小由高度、宽度决定，包括所有内边距和滚动条和边框大小，注意不包括外边距

* offsetHeight 元素在垂直方向上占用的空间大小，以像素计，包括元素的高度，可见的水平滚动条的高度，上下边框的高度
* offsetWidth:元素在水平方向上占用的空间大小，以像素计，包括元素的宽度，可见的垂直滚动条的高度，左右边框的高度
* offsetLeft: 元素的左边框至包含元素的左内边框之间的像素距离
* offserTop: 元素的上边框至包含元素的上内边框之间的像素距离

**客户区大小**

指的是元素内容及内边距所占据的空间大小，clientWidth clientHeight

* clientWidth 元素内容区宽度+左右内边距的值
* clientHeight 元素内容去高度+上下内边距的值

**滚动大小**
    
包含滚动内容的元素的大小

* scrollHeight: 在没有滚动条的情况下，元素内容的总高度
* scrollWidth 在没有滚动条的情况下，元素内容的总宽度
* scrollLeft 被隐藏在内容区域左方的像素数
* scrollTop 被隐藏在内容区域上方的像素数

**确定元素大小**

element.getBoundingClientRect()

返回：
top
left
bottom
right
width
height

## 事件

**事件流**

事件流描述的是从页面中接收事件的顺序。IE的事件流是事件冒泡流，Netscape的事件流是事件捕获流

DOM2级事件规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段

**事件处理程序**

DOM0级事件处理程序，将一个函数赋值给一个事件处理程序属性

DOM2级事件处理程序，定义了两个方法用于处理指定和删除事件处理程序的操作，addEventListener() removeEventListener()

**IE事件处理程序**

IE实现了与DOM中类似的两个方法：attachEvent detachEvent 这两个方法接收相同的两个参数：事件处理程序名称和事件处理程序函数，因为IE8及更早版本只支持冒泡，所以通过attachEvent 添加的事件处理程序都会被添加到冒泡阶段

**事件对象**

再出发DOM上的某个事件时，会产生一个事件对象event，这个对象中包含着所有与事件相关的信息（包括导致事件的元素、类型以及其他与特定事件相关的信息）

IE中的事件对象即event对象，在使用DOM0级方法添加事件处理程序时，event对象作为window对象的一个属性存在

```
    var EventUtil = {
        addHandler: function(elem, type, handler) {
            if(elem.addEventListener) {
                elem.addEventListener(type, handler);
            } else if(elem.attachEvent) {
                elem.attachEvent('on' + type, handler);
            } else {
                elem['on' + type] = handler;
            }
        },
        removeHandler: function(elem, type, handler) {
            if(elem.removeEventListener) {
                elem.removeEventListener(type, handler);
            } else if(elem.detachEvent) {
                elem.detachEvent('on' + type, handler);
            } else {
                elem['on' + type] = handler;
            }
        },
        getEvent: function() {
            return event ? event : window.event;
        },
        stopPropagation: function(event) {
            if(event.stopPropagation) {
                event.stopPropagation();
            } else {
                event.cancelBubble = true;
            }
        },
        preventDefault: function(event) {
            if(event.preventDefault) {
                event.preventDefault();
            } else {
                event.returnValue = false;
            }
        },
        getTarget: function(event) {
            return event.target || event.srcElement;
        }
    }
```
**事件类型**

“DOM3级事件”规定了以下几类事件：

* UI事件，当用户与页面上的元素交互时触发
    
    * load事件，当页面完全加载完，包括所有图像等其他静态文件，就会触发window上的load事件。
    * unload事件，这个事件在文档被完全卸载后触发。只要用户从一个页面触发到另外一个页面就会触发。常用来清除引用，防止内存泄漏。
    * resize事件，当浏览器窗口被调整到了一个新的高度或宽度时，就会触发resize事件，这个事件在window上面触发
    * scroll事件，虽然scroll时间是在window对象上出发，但它实际表示的则是页面相应元素的变化
    
* 焦点事件
    
    焦点从页面中的一个元素移动到另一个元素：
        
    * focusout 失去焦点元素
    * focusin 获得焦点元素
    * blur  （不冒泡）
    * DOMFocusOut （Opera浏览器）
    * focus （不冒泡）
    * DOMFocusIn

* 鼠标事件
    
    * click
    * dblclick
    * mousedown
    * mouseenter 不冒泡
    * mouseleave 不冒泡 只有在鼠标指针离开被选元素时，才会触发 mouseleave 事件
    * mousemove
    * mouseout 不论鼠标指针离开被选元素还是任何子元素，都会触发 mouseout 事件
    * mouseover
    * mouseup
    
    事件对象中的button属性表示鼠标按钮
    
    在触摸设备
    
    * 不支持dblclick事件，双击浏览器窗口会放大页面，而且没有改变行为
    * 轻击可单击元素会触发mousemove事件，如果屏幕没有变化，则会依次产生mousedown mouseup和click事件

* 滚轮事件
* 文本事件
* 键盘事件

    * kyedown
    * keypress
    * keyup

    event对象的keyCode属性会包含一个代码，与键盘上一个特定的键对应
    
* 合成事件,当为IME（输入法编辑器）输入字符时触发
* 变动事件，当底层DOM结构发生变化时触发

    * DOMSubtreeModified 在DOM结构中发生任何变化时触发，这个事件在其他任何事件触发后都会触发
    * DOMNodeInserted  在一个节点作为子节点被插入到另一个节点被触发
    * DOMNodeRemoved 在节点从父节点移除时触发
    * DOMNodeInsertedIntoDocument 在DOMNodeInserted后触发
    * DOMNodeRemovedFromDocument 在DOMNodeRemoved后触发

    * DOMAttrModified 特性被修改
    * DOMCharacterDataModified 文本节点被修改

* HTML5事件

    * DOMContentLoaded事件，window的load事件会在页面中的一切都加载完毕时触发，但这个过程中可能会因为要加载的外部资源过多而耗时长，而DOMContentLoaded事件则在形成完整的DOM树之后就会触发
    * readystatechange事件，支持readystatechange事件的每个对象都会有一个readyState属性

        * uninitialized. 未初始化
        * loading 正在加载
        * loaded 加载完毕
        * interactive 交互
        * complete 完成
        
    * hashchange事件，event.oldURL,event.newURL


    

