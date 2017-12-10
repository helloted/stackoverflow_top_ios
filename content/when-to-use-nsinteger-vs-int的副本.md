# NSOperation vs. GCD？
[NSOperation vs Grand Central Dispatch](https://stackoverflow.com/questions/10373331/nsoperation-vs-grand-central-dispatch)

___



> 1

`GCD` 是更底层 API.
`NSOperation` 和 `NSOperationQueue` 是 Objective-C 类.
`NSOperationQueue` 基于`GCD`. 如果你在用NSOperation, 那你是隐式使用 *Grand Central Dispatch.*

**GCD 相比 NSOperation的优势:**
*i. implementation*
 `GCD` 的声明很轻量
`NSOperationQueue` 复杂和重量级

*ii. 效率*

当使用NSOperations和NSOperationQueues时，会有一些不必要的开销。 这些是Cocoa对象，他们需要分配和释放。

**NSOperation 相比 GCD的优势:**

*i.  Operation控制*
你可以暂停(Pause), 取消(Cancel), 恢复(Resume) 一个 `NSOperation`

*ii. 依赖*
你可以在两个 `NSOperations`之间建立依赖
operation 不会开始直到它的依赖已经完成了.

*iii. Operation状态*
可以监听operation的状态. 就绪(ready) ,执行中(executing)和完成(finished)

*iv.  Operation最大数*
你可以指定 operations同时操作的数量

**什么时候用 GCD or NSOperation**
如果你想对Queue有更多的操作，你应该使用 `NSOperation` 

如你想要轻量方便地使用，就应该用 `GCD`