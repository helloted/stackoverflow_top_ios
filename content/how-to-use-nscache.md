# 如何使用NSCache?
[How to use NSCache](https://stackoverflow.com/questions/5755902/how-to-use-nscache)

___



> 1

你可以像使用 `NSMutableDictionary`一样使用`NSCache` . 不同的是当`NSCache` 内存超出压力 (比如缓存了太多) 它会释放一些值来保留空间。

如果你可以重建这些值 (通过互联网下载, 计算, 其他方式) ，那么 `NSCache` 可能适合你. 但是如果数据不可复现 (比如用户输入，数据对时间敏感) ，那你不应该存在 `NSCache` 因为这些数据有可能会被消失。

```objc
// 你的缓存应该具有超出某个方法的生命周期，可以伴随着application,delegate或者Viewcontroller.
NSCache *myCache = ...;
NSAssert(myCache != nil, @"cache object is missing");

// 从缓存里获取，如果存在的话
Widget *myWidget = [myCache objectForKey: @"Important Widget"];
if (!myWidget) {
	// 有可能没有放入缓存，或者已经被移除了，那么就应该重新建立
    myWidget = [[[Widget alloc] initExpensively]];

	// 放入缓存中
    [myCache setObject: myWidget forKey: @"Important Widget"];
}

// 这样无论如何myWidget都是有的
if (myWidget) {
    [myWidget runOrWhatever];
}
```