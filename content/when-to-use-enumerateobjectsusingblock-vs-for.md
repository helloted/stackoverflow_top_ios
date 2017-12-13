# for vs. enumerateObjectsUsingBlock
[When to use enumerateObjectsUsingBlock vs. for](https://stackoverflow.com/questions/4486622/when-to-use-enumerateobjectsusingblock-vs-for)

___



> 1

根据上下文来选择你需要的遍历模式

 `for(... in ...)` 使用方便，句法简洁。

`enumerateObjectsUsingBlock:` 有一些你会认为有趣或者无趣的特点。

- `enumerateObjectsUsingBlock:` 会比for循环更快 (`for(... in ...)` 用的是 `NSFastEnumeration` 进行快速枚举). For循环需要从内部表示转变到快速枚举的表示，这样会有瓶颈。 基于块的枚举允许集合类以尽可能快的方式枚举内容，快速遍历本地存储格式。对于数组来说可能差别不大，但是对于字典会有很大的区别。
- "当你需要修改局部变量的时候不要用enumerateObjectsUsingBlock" - 这句话是不对的，因为你可以用 `__block` 来修饰变量，这样的话就可以修改变量。
- `enumerateObjectsWithOptions:usingBlock:` 支持方向或者正向遍历。
- 用字典的话，基于块的枚举是同时检索关键字和值得唯一方法。


> 2

GCD apply也支持循环遍历

```objc
dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_HIGH, 0);
dispatch_apply([array count], queue, ^(size_t idx) {
    id obj = [array objectAtIndex: idx];
    /* Do something with |obj|. */
});
```

