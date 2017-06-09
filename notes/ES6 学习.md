# ES6 学习

* class

---------------------
类的内部所有定义的方法，都是不可枚举的,这一点与ES5的行为不一致

constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法，一个类必须有constructor方法，如果没有显示定义，一个空的constructor方法会被默认添加

class不存在变量提升

ES6不提供私有方法,可以利用Symbol的方式来实现私有方法


```
const bar = Symbol('bar');
const snaf = Symbol('snaf');

class myClass {
    foo(baz) {
        this[bar](baz);
    }

    [bar](baz) {
        return this[snaf] = baz;
    }
}
```

类的方法内部如果含有this，他默认指向类的实例。但是必须非常小心，一旦单独使用该方法，很可能会报错

name属性

--------------
const定义常量的原理是阻隔变量名所对应的内存地址被变化

const定义的对象常量，其内容依然能够通过修改属性值而被修改。可以使用freeze来使首层的属性不改变。若实现完全不会改变的对象可以通过小工具创建


