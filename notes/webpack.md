# webpack
webpack是前端构建工具

默认配置文件是`webpack.config.js`


--------
学习点：

**CSS Module**

css-loader?modules 

CSS Modules 允许使用`:global(.className)`的语法，声明一个全局规则，凡是这样声明的class都不会被编译成哈希字符串

 **webpack.DefinePlugin插件**

    通过设置环境标志符来使一些代码在开发环境中有效
    
    ```
        //main.js
        document.write('<h1>Hello World</h1>');
        if(__DEV__){
            document.write(new Date());
        }
        //webpack.config.js
        var webpack = require('webpack');
        var devFlagPlugin = new webpack.DefinePlugin({
            __DEV__: JSON.stringify(JSON.parse(process.env.DEBUG || 'false'))
        });
        module.exports = {
            entry: './main.js',
            output: {
                filename: 'bundle.js'
            },
            plugins: [devFlagPlugin]
        }
    ```

**代码分块(Code splitting)**

实现按需加载

对于大型的web应用来说，将所有的代码放入到一个文件中不是高效的，webpack允许你将它们分片到成几块，特别是在某些情况下，只需要一些代码块，这些代码块就可以按需加载

[按需加载代码](https://github.com/ruanyf/webpack-demos#demo12-common-chunk-source)


**HMR 热加载**

`webpack-dev-server --hot --inline`

`--hot` 增加 HotModuleReplacementPlugin插件以及切换到热模式

`--inline`将webpack-dev-server运行时嵌入到bundle文件中

`--hot --inline` 加入webpack/hot/dev-server入口

等同于下面的webpack.config.js配置

```
var webpack = require('webpack');
var path = require('path');

module.exports = {
    entry: [
        'webpack/hot/dev-server',
        'webpack-dev-server/client?http://localhost:8080',
        './index.js'
    ],
    output:{
        filename: 'bundle.js',
        publicPath: '/static/'
    },
    plugins:[
        new webpack.HotModuleReplacementPlugin()
    ],
    module: {
        loaders: [{
            test: /\.jsx?$/,
            exclude: /node_modules/,
            loader: 'babel-loader',
            query: {
                presets: ['es2015', 'react']
            },
            include: path.join(__dirname, '.')
        }]
    }
}

//launch
webpack-dev-server
```

**但使用react-router时**

使用 --history-api-fallback

`webpack-dev-server --history-api-fallback`


**可以使用CommonsChunkPlugin将公共部分抽离成一个文件**

```
//main1.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
    <h1>hello</h1>,
    document.getElementById('a')
);

//main2.jsx

var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
    <h1>hello2</h1>,
    document.getElementById('b')
);

//index.html
<html>
  <body>
    <div id="a"></div>
    <div id="b"></div>
    <script src="init.js"></script>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>

//webpack.config.js
var CommonsChunkPlugin = require('webpack/lib/optimeze/CommonsChunkPlugin');
module.exports = {
    entry: {
        bundle1: './main1.jsx',
        bundle2: './main2.jsx'
    },
    output: {
        filename: '[name].js'
    },
    module: {
        loaders: [{
            test: /\.js[x]?$/,
            exclude: /node_modules/,
            loader: 'babel-loader',
            query: {
                presets: ['es2015', 'react']
            }
        }]
    },
    plugins: [
        new CommonsThunkPlugin('init.js')
    ]
}
```

**可以使用externals来暴露全局变量**

[链接](https://github.com/ruanyf/webpack-demos#demo14-exposing-global-variables-source)

```
//data.js
var data = 'hello';

//webpack.config.js

module.exports = {
    entry: './main.jsx',
    output: {
        filename: 'bundle.js'
    },
    module: {
        loaders: [{
            test: /\.js[x]?$/,
            exclude: /node_modules/,
            loader: 'babel-loader',
            query: {
                presets: ['es2015','react']
            }
        }]
    },
    externals: {
        data: 'data'
    }
}

// main.jsx
var data = require('data');
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>{data}</h1>,
  document.body
);
```



## webpack 的性能优化



