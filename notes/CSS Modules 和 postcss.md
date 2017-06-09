# CSS Modules 和 postcss
[css Modlues](https://zhuanlan.zhihu.com/p/20495964?refer=purerender)

[css Modules](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)


css模块化，解决了平时的css所带来的一些问题

*  全局污染
CSS 使用全局选择器机制来设置样式，优点是方便重写样式。缺点是所有的样式都是全局生效，样式可能被错误覆盖，因此产生了非常丑陋的 `!important`，甚至 inline `!important` 和复杂的[选择器权重计数表](Selectors Level 3)，提高犯错概率和使用成本。Web Components 标准中的 Shadow DOM 能彻底解决这个问题，但它的做法有点极端，样式彻底局部化，造成外部无法重写样式，损失了灵活性。

*  命名混乱

由于全局污染的问题，多人协同开发时为了避免样式冲突，选择器越来越复杂，容易形成不同的命名风格，很难统一。样式变多后，命名将更加混乱。

*  依赖管理不彻底

组件应该相互独立，引入一个组件时，应该只引入它所需要的 CSS 样式。但现在的做法是除了要引入 JS，还要再引入它的 CSS，而且 Saas/Less 很难实现对每个组件都编译出单独的 CSS，引入所有模块的 CSS 又造成浪费。JS 的模块化已经非常成熟，如果能让 JS 来管理 CSS 依赖是很好的解决办法。Webpack 的 `css-loader` 提供了这种能力。

*  无法共享变量

复杂组件要使用 JS 和 CSS 来共同处理样式，就会造成有些变量在 JS 和 CSS 中冗余，Sass/PostCSS/CSS 等都不提供跨 JS 和 CSS 共享变量这种能力。

* 代码压缩不彻底

由于移动端网络的不确定性，现在对 CSS 压缩已经到了变态的程度。很多压缩工具为了节省一个字节会把 '16px' 转成 '1pc'。但对非常长的 class 名却无能为力，力没有用到刀刃上。



# postcss
postcss是一种通过js的插件来改变css的工具集合。这些插件包括变量还有混合以及对未来css的支持

postcss是将css转化成一种js可以操作的数据格式，他不会直接改变你的css，它只是为很多改变css操作css的js插件提供了平台，铺平了道路

## 对postcss的一些误解
* 它不是一种css预处理器
* 它不是一个css后处理器
* 它不是css的未来语法
* 它不是一个优化的工具


* In this intro we covered what PostCSS is NOT:
    * It’s not a pre-processor, though it can optionally behave like one.
    * It’s not a post-processor, though it can optionally behave like one.
    * It’s not about “future syntax”, though it can facilitate support for future syntax
    * It’s not a clean up / optimization tool, though it can provide such functionality.
    * It’s not any one thing; it’s a means to potentially unlimited functionality configured as you choose.
* We also covered what makes PostCSS special:

    *   The diverse functionality available via its plugin ecosystem
    * Its modular, “use what you need” nature
    * Its rapid compilation time
    * The accessibility of creating your own plugins
    * The option to use it with regular CSS
    * The ability to create libraries that don’t depend on one preprocessor
    * Its seamless deployment with many popular build tools


