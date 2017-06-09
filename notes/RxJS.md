# RxJS

Rx 的编程模型实际是基于 Observer pattern 和 Iterator pattern 这两种设计模式构建的。

基于 Observable 的模式， 和传统的 Observer pattern有两点本质的不同：

Observable 只在至少有一个订阅者时，数据才开始流动
在数据流结束（iterator 不再hasNext）时，Observable会发出通知（onCompleted）

Observables 作为被观察者，是一个值或事件的流集合；而 Observer 则作为观察者，根据 Observables 进行处理。

订阅：Observer 通过 Observable 提供的 subscribe() 方法订阅 Observable。
发布：Observable 通过回调 next 方法向 Observer 发布事件。

观察者和被观察者，如果被观察者发生了变化后，会通知观察者。




