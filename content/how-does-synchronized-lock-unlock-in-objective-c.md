# @synchronized是如何加锁/解锁？
[How does @synchronized lock/unlock in Objective-C?](https://stackoverflow.com/questions/1215330/how-does-synchronized-lock-unlock-in-objective-c)

___



> 1

Objective-C语言里synchronization用的是互斥锁，就如同 `NSLock` . 虽然在有一些小的技术差异，但把它们看作在一个共同的（更原始的）实体之上实现的两个单独的接口是可以的。

特别地，如果用 `NSLock` 你有一个明确的锁，而如果用 `@synchronized` 你有一个隐含的锁与你需要同步的对象相关联. 编译可以明白，在实际操作上基本上是一样的.

你可以认为 `@synchronized` 会被编译器改写成:

```objc
- (NSString *)myString {
  @synchronized(self) {
    return [[myString retain] autorelease];
  }
}
```

被转换成

```objc
- (NSString *)myString {
  NSString *retval = nil;
  pthread_mutex_t *self_mutex = LOOK_UP_MUTEX(self);
  pthread_mutex_lock(self_mutex);
  retval = [[myString retain] autorelease];
  pthread_mutex_unlock(self_mutex);
  return retval;
}
```

这个并不完全准备，因为实际转换会更复杂而且用上了递归锁，但是你应该可以看到重点。

> 2

在Objective-C, 一个 `@synchronized` block自动处理了加锁和解锁的操作. 运行时会自动生成一个递归锁NSRecursiveLock加在你想要同步的对象上面. 这就是为什么你没有看到你的NSLock子类的日志消息 - 你同步的对象可以是任何东西，而不仅仅是一个NSLock。

一般来说, `@synchronized (...)` 是一个很方便的结构让你的代码顺畅化. 就如果大多数简化的抽象一样，会有一些开销。但是，当你用这样的结构时，原始的性能应该不是作为最高的目标