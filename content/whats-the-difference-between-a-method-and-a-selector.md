# Method vs. selector vs. IMP
[What's the difference between a method and a selector?](https://stackoverflow.com/questions/5608476/whats-the-difference-between-a-method-and-a-selector)

___



> 1

- **Selector** - 一个Selector是一个方法的名字. 你应该对这些selectors很熟悉: `alloc`, `init`, `release`, `dictionaryWithObjectsAndKeys:`, `setObject:forKey:`, 注意，冒号是selector的一部分，用来定义我们需要的参数. 甚至于(尽管很少， Cocoa frameworks看不到), 你可以有一个selectors 像这样 `doFoo:::`. 这是一个方法需要三个参数，你可以这样调用 `[someObject doFoo:arg1 :arg2 :arg3]`，也就是没有必要再每个参数前面都要有字母。 你可以直接使用selectors在Cocoa. 有相应的类型 `SEL`: `SEL aSelector = @selector(doSomething:)` or `SEL aSelector = NSSelectorFromString(@"doSomething:");`
- **Message** - 消息，是在Runtime时，selector和对应的参数被发送的消息. 消息可以封装在一个 `NSInvocation` 对象里供以后调用. 消息会被发送给一个 *receiver*. (对象会接受这个消息).
- **Method** - 方法是selector和一个声明的联合.  "声明" 是一个函数指针 (an `IMP`). 一个实际的方法可以在内部使用一个Method结构体来检索（可以从运行时检索到）。


- **Method Signature** - 方法签名表示由方法返回并接受的数据类型。 它们可以在运行时通过NSMethodSignature和（在某些情况下）一个原始char *来表示。
- **Implementation** -方法的实际执行代码. 在运行时的类型是 `IMP`, 是一个函数指针. 