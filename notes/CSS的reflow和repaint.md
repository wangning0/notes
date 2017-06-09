# CSS的reflow和repaint

## 比较
repaint是重绘 reflow是回流
前者是指针对某个DOM元素进行重新重绘制
后者是指针对整个页面的重排，也就是页面所有DOM的渲染
## 什么是reflow
浏览器为了重新渲染部分或整个页面，重新计算页面元素位置和几何结构的进程叫做`reflow`.

通俗点说就是当开发人员定义好了样式后(也包括浏览器的默认样式),浏览器根据这些来计算并根据结果将元素放到它应该出现的位置上，这个过程叫做`reflow`.

由于`reflow`是一种浏览器中的用户拦截操作，所以我们了解如何减少reflow次数，及DOM的层级，css效率对refolw次数的影响是十分有必要的。

reflow(回流)是导致DOM脚本执行效率低的关键因素之一，页面上任何一个节点触发了reflow，会导致它的子节点及祖先节点重新渲染。

```
<body>
  <div class="hello">
    <h4>hello</h4>
    <p><strong>Name:</strong>BDing</p>
    <h5>male</h5>
    <ol>
      <li>coding</li>
      <li>loving</li>
    </ol>
  </div>
</body>
```

当p节点上发生reflow时，hello和body也会重新渲染，甚至h5和ol都会收到影响。

### 什么时候会导致reflow发生呢？
* 改变窗口大小
* 改变文字大小
* 添加/删除样式表
* 内容的改变，(用户在输入框中写入内容也会)
* 激活伪类，如:hover
* 操作class属性
* 脚本操作DOM
* 计算offsetWidth和offsetHeight
* 设置style属性
```
clientHeight, clientLeft, clientTop, clientWidth, focus(), getBoundingClientRect(), getClientRects(), innerText, offsetHeight, offsetLeft, offsetParent, offsetTop, offsetWidth, outerText, scrollByLines(), scrollByPages(), scrollHeight, scrollIntoView(), scrollIntoViewIfNeeded(), scrollLeft, scrollTop, scrollWidth
```

### 减少reflow对性能的影响的建议
* 尽可能限制reflow的影响范围，尽可能在低层级的DOM节点上，上述例子中，如果你要改变p的样式，class就不要加在div上，通过父元素去影响子元素不好。
* 避免设置大量的style属性，因为通过设置style属性改变结点样式的话，每一次设置都会触发一次reflow，所以最好是使用class属性
* 实现元素的动画，它的position属性，最好是设为absoulte或fixed，这样不会影响其他元素的布局
* 动画实现的速度的选择。比如实现一个动画，以1个像素为单位移动这样最平滑，但是reflow就会过于频繁，大量消耗CPU资源，如果以3个像素为单位移动则会好很多。
* 不要使用table布局，因为table中某个元素旦触发了reflow，那么整个table的元素都会触发reflow。那么在不得已使用table的场合，可以设置`table-layout:auto;`或者是`table-layout:fixed`这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围
* 如果CSS里面有计算表达式，每次都会重新计算一遍，出发一次reflow
* 离线批量处理dom改变，离线意味着不要在当前的dom树中操作，你可以
    * 1 通过documentFragment处理临时操作
    *  把你即将进行操作的节点复制出来，操作副本，然后替换即将要操作的节点
    *  用display：none把节点藏起来(一次reflow,一次repaint),添加完大量的操作，重新展示（一次reflow，一次repaint），用这种方式你可以只渲染两次，大大减少渲染次数


## 什么是repaint

repaint是在一个元素的外观被改变，但没有改变布局的情况下发生的，如改变了visibility、outline、background等。当repaint发生时，浏览器会验证DOM树上所有其他节点的visibility属性。

通俗来说，就是当各种盒子的位置、大小以及其他属性，例如颜色、字体都确定下来后，浏览器便把这些元素都按照各自的特性绘制一遍，于是页面的内容出现了，这个过程叫做repaint

## 什么会触发refolw或者repaint
任何改变用于构建渲染树的初始化信息的都会触发reflow或者repaint,比如：

* 添加、删除、改变dom节点
* 通过display: none隐藏一个节点（触发reflow and repaint）以及通过visibility: hidden隐藏节点（仅触发repaint
* 移动或者给一个节点添加动画
* 添加一个样式，或者调整样式
* 用户操作比如调整窗口大小，改变字体大小，或者滚动等



