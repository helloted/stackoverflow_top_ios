# Block作为参数传递
[Objective-C pass block as parameter](https://stackoverflow.com/questions/7936570/objective-c-pass-block-as-parameter)

___



> 1

block变量取决于它的参数和返回值，一般情况下，block声明和函数声明差不多。把 `*` 换成 `^`：

```
- (void)iterateWidgets:(void (^)(id, int))iteratorBlock;
```

这种看起来有点乱，你可以先进行声明

```
typedef void (^ IteratorBlock)(id, int);
```

```
- (void)iterateWidgets:(IteratorBlock)iteratorBlock;
```