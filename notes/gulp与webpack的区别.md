# gulp与webpack的区别
其实webpack展示具有前端构建的功能而已，其实本质来说webpack是一种模块化的解决方案，只不过通过插件实现了构建工具的一些功能。

gulp是通过一系列插件将原本复杂繁琐的任务自动化，是一个纯粹的工具，它并不能将你的css等非js资源模块化，但是webpack可以做到这些。它是一种工具，能够优化前端工作流程(刷新页面，压缩css、js、编译less等)

seajs和require是一种在线“编译”模块的方案，相当于在页面上加载了一个cmd/amd解释器，这样浏览器就认识了define、exports、module这些东西，也就实现了模块化

browserify和webpack是一种预编译模块的方案，不需要在浏览器中加载解释器，它可以编译称浏览器认识的js

所以你可以通过gulp去配置webpack的文件




