# React的学习啊！！

## Component 生命周期

**总体分为三个板块，Mounting,Updating,Unmounting**

* getInitialState()
* componentWillMount()
* componentDidMount()
* componentWillReceiveProps(object nextProps)
* shouldComponentUpdate(object nextProps, object nextState)
* componentWillUpdate(object nextProps, object nextState)
* componentDidUpdate(object preProps, object prevState)
* componentWillUnmount

## 虚拟DOM
虚拟DOM是一个js的树形结构，包含了React元素和模块。组件的DOm结构就是映射到对应的虚拟DOM上，React通过渲染虚拟DOM到浏览器，使得用户界面的一显示。React在虚拟的DOM上实现了一个diff算法，当要更新组件的时候，会通过diff寻找到要变更的DOM节点，再把这个修改更新到浏览器实际的DOM节点上。

## redux
* 应用中所有的state都以一个对象树的形式储存在一个单一的store中
* 唯一改变state的办法就是触发action，一个描述发生什么的对象
* 为了描述action如何改变state树，你需要编写reducers
* 三大原则

    * 单一的数据源，整个应用的state被储存在一棵object tree中，并且这个object tree只存在唯一一个store中
    * State是只读的，唯一改变state的方法就是触发action，action是一个用于描述已发生事件的普通对象
    
    * 使用纯函数来执行修改，为了描述action如何改变state tree，需要编写reducers,Reducer只是一些纯函数，他接受先前的state和action，并返回新的state

* action创建函数
        
        ```
        function addTodo(text) {
        return {
            type: ADD_TODO,
        text
        }
        ```

* react-redux中提供的connect()帮助器会帮你调用dispatch()方法.bindActionCreators()可以自动把多个action创建函数绑定到dispatch()方法上
* 永远不要在reducer里做以下操作

    * 修改传入参数
    * 执行有副作用的操作，如API请求和路由跳转
    * 调用非纯函数，如Date.now(),或Math.random()
* Store有以下职责    
    * 维持应用的state
    * 提供getState()方法获取state
    * 提供dispatch(action)方法更新state
    * 通过subscribe(listener注册监听器)
    * 通过unsubscribe(listener)返回的函数注销监听器
* Redux应用中的数据的生命中期遵循下面4个步骤
    * 调用 store.dispatch(action)，你可以在任何地方调用store.dispatch(action),包括组件中，XHR回调中、甚至是定时器中
    * Redux store调用传入的reducer函数，store会把两个参数传入reducer，当前的state树和action
    * 根reducer应该把多个子reducer输出合并成一个单一的state树，根reducer的结构完全由你决定，Redux原生提供combineReducers()辅助函数，来把根reducer拆分成多个函数，用于分别处理state树的一个分支
    * Redux store保存了根reducer返回的完整的state树
    * 任何一个从`connect()`包装好的组件都可以得到一个dispatch方法作为组件的props，以及得到全局state中所需的任何内容。connect()的唯一参数是selector，此方法可以从Redux store接收到全局的state，然后返回组件中需要的props，最简单的情况下，可以返回一个初始的state

## 深入浅出React系列

* 所谓组件，就是状态机器，React将用户界面看作简单的状态机器，当组件处于某个状态时，那么就输出这个状态对应的界面，通过这种方式，就很容易去保证界面的一致性
* Flux提倡的是单向数据流动，即永远只有从模型道视图的数据流动
* Flux引入了Dispatcher和Action的概念，Dispatcher是一个全局的分发器负责接收Action，而Store可以在Dispatcher上监听道Action并做出相对应的操作。类似于全局的订阅发布模式
* 组件的生命周期
    
    ```
        //first render
        getDefaultProps->getInitialState->componentWillMount->render->componentDidMount
        //props change
        componentWillReceiveProps->shouldComponentUpdate->componentWillUpdate->render->componentDidUpdate
        //state change
        shouldComponentUpdate->componentWillUpdate->render->componentDidUpdate
        //unmount
        componentDidUnmount
    ```
    
* 删除节点意味着彻底销毁该节点，而不是再后续的比较中再去看是否有另外一个节点等同于该删除的节点。如果该删除节点之下有子节点，那么这些子节点也会被完全删除。它们也不会用于后面的比较



