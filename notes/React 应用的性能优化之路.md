# React 应用的性能优化之路
[链接](https://segmentfault.com/a/1190000006254212)
[链接](https://segmentfault.com/a/1190000006100489)
[链接](http://shenzm.cn/blog/message.14)
React应用主要的性能在与多余的处理和组件的DOM对比。为了避免这些性能陷阱，你应该尽可能的在shouldComponentUpdate中返回false
    
**加速shouldComponentUpdate的检查** 
**简化shouldComponentUpdate的检查**

React应用的主要性能问题是什么？

* 组件中那些不更新DOM的冗余操作
* DOM比较那些无需更新的叶子结点

因为在JS中的对象是不相等的，因为会比较地址，所以这个时候，最初的想法是会在shouldComponentUpdate中进行深度对比来确保改变的正确跟踪，但是这个方法在性能上的花费是很大的，因为我们需要为每个model写不同的深度对比代码。

```
    //字符串很容易去实现
    React.createClass({
        propTypes: {
            value: React.PropTypes.string.isRequired
        },
        shouldComponentUpdate: function(nextProps, nextState) {
            return this.props.value !== nextProps.value;
        },
        render: function() {
            return <div>{this.props.value}</div>
        }
    })
    //Object就不行
    React.createClass({
        propTypes: {
            value: React.PropTypes.object.isRequired
        },
        shouldComponentUpdate: function(nextProps, nextState) {
            return this.props.value !== nextProps.value;
        },
        render: function() {
            return <div>{this.props.value}</div>
        }
    })
```

实际上this.props.value和nextProps.value是同一个对象的引用

解决方案是利用Immutable-js


--------------

**Q:** 如果更新的props和旧的一样，那么这个时候很明显UI不会变化，但是react还是要进行虚拟DOM的diff，这个diff就是多余的性能损耗，而且在DOM结构比较复杂的情况，整个diff会花费比较长的时间
**A:** react给我们提供了PureRenderMixin,如果react组件是纯函数的，就是给组件相同的props和state组件就会展现同样的UI，可以使用这个Minxin来优化React的组件性能

```
    var PureRenderMixin = require('react-addons-pure-render-mixin');
    React.createClass({
        mixins: [PureRenderMixin],
        render: function() {
            return <div className={this.props.className}>foo</div>
        }
    })
```
**ES6的写法**

```
    import PureRenderMixin from 'react-addons-pure-render-mixin';
    class FooComponent extends React.Component {
        constructor(props) {
            super(props)l
            this.shouldComponentUpdate = PureRenderMixin.shouldCompoentUpdate.bind(this);
        }
        
        render() {
            return <div className={this.props.className}>foo</div>
        }
    }   
```
**原理就是它实现了shouldComponentUpdate，在函数内比较当前的props、state是否相等**

**注意的是PureRenderMixin内进行的仅仅是浅比较对象，如果对象包含了复杂的数据结构，深层次的差异可能出现误判，仅仅用于简单的props和state组件**

**复杂的props和sttae的情况下，要使用immutable.js**

-----------

**Q:** PureRenderMixin和shouldComponentUpdate的关注点是UI需不需要更新，而render则更多关注虚拟DOM的diff规则了，如何让diff结果最小化、过程最简化是render内优化的关注点?
**A:** 1、diff算法将不会尝试匹配不同组件类的子树。如果发现正在使用的两个组件类输出的 DOM 结构非常相似，你可以把这两个组件类改成一个组件类。

2、如果没有提供稳定的key（例如通过 Math.random() 生成），所有子树将会在每次数据更新中重新渲染。

**组件的key属性也可以带来性能的优化,它的作用就是给React提供了一种除组件类之外识别一个组件的方法**举个例子：一个父组件中有按照顺序排列好的img子组件，这是，在队列中间又一个插入img组件的操作，如果没有key属性，在渲染的时候会导致插入项的后续img表情的src属性都发生了改变，但是如果有key的话，并且key是独一无二的，这样就不会在渲染的时候，改变其他的src属性了，而是用了DOM的insertBefore操作，所以说**key属性能帮助React识别列表子组件的最小变化，从而提升高效的DOM操作**




