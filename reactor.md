# 1. Mono与Flux
> https://www.cnblogs.com/felordcn/p/13747262.html
- Mono和Flux是流式范式（reactive Streams），这种范式让数据具有一些新特性，比如基于发布订阅的事件驱动，异步流，背压等
- Push的模式，有别于以前Pull的模式
  - 在传统的编程范式中，我们一般通过迭代器（Iterator）模式来遍历一个序列。这种遍历方式是由调用者来控制节奏的，采用的是拉的方式。每次由调用者通过 next()方法来获取序列中的下一个值。使用反应式流时采用的则是推的方式，即常见的发布者-订阅者模式。当发布者有新的数据产生时，这些数据会被推送到订阅者来进行处理。在反应式流上可以添加各种不同的操作来对数据进行处理，形成数据处理链。这个以声明式的方式添加的处理链只在订阅者进行订阅操作时才会真正执行
- 对Mono与Flux的map和flatMap类似于java Stream
  - Java 流通常是同步的，同时只能处理有限数据集。它们本质上是使用函数式进行集合迭代的一种手段。响应式流支持任何大小的数据集，包括无限数据集的异步处理。它们使实时处理数据成为了可能   


But how can you produce asynchronous code on the JVM? Java offers two models of asynchronous programming:

- Callbacks: Asynchronous methods do not have a return value but take an extra callback parameter (a lambda or anonymous class) that gets called when the result is available. A well known example is Swing’s EventListener hierarchy.

- Futures: Asynchronous methods immediately return a Future<T>. The asynchronous process computes a T value, but the Future object wraps access to it. The value is not immediately available, and the object can be polled until the value is available. For instance, an ExecutorService running Callable<T> tasks use Future objects.


 In Reactor, operators are the workstations in our assembly analogy. Each operator adds behavior to a Publisher and wraps the previous step’s Publisher into a new instance. 
  所以flatMap和map返回的仍然是Publisher，并且与之前的不是一个Publisher
 [see this item](https://projectreactor.io/docs/core/release/reference/#faq.chain)

 Unless specified, the topmost operator (the source) itself runs on the Thread in which the subscribe() call was made
