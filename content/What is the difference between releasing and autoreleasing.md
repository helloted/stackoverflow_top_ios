# autorelease和release有什么区别？
[What is the difference between releasing and autoreleasing?](https://stackoverflow.com/questions/2076402/what-is-the-difference-between-releasing-and-autoreleasing)

___



> 1

release意味着会被马上释放，autorelease则是将对象放入autorelasepool中，只有当autorelasepool被drain时才会被release，延迟释放。

为什么需要autorelease？

先看relase

```Objc
-(void)someMethod{
  MyObject *obj = [MyObject new];
  
  //用obj做一些事情
  ...
  
  [obj release]
}
```

这种情况下，先持有然后再释放，obj的内存在方法结束后就被回收。就能保证内存不泄露。

但是如果这个对象在方法结束后还要继续用，就不能当即释放了，但是不release，又会造成内存泄漏。

```Objc
- (MyObject *)myMethod {
    MyObject *obj = [MyObject new];
  
  //用obj做一些事情
  ...
  
  [obj autorelease];
  return obj;
}
```

这种情况下，obj暂时不会被释放

```
- (void)someOtherMethod {
...
MyObject *aobj = [Instance myMethod];

}
```

aobj指向的内存，与obj一样的内存，在autoreleasepool被drain时才会回回收释放。保证内存不泄漏的同时还能保持使用。

