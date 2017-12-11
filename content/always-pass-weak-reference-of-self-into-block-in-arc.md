# 往ARC的Block传值一定要弱引用么？
[Always pass weak reference of self into block in ARC?](https://stackoverflow.com/questions/20030873/always-pass-weak-reference-of-self-into-block-in-arc)

___



> 1

一个循环引用产生时因为当A对象retains对象B，并且对象B retains 对象A，在这种情况下，如果其中一个对象被released:

- 对象A不会被dealloc因为对象B强引用了它
- 但是对象B也不会被dealloc同样因为对象A引用了它
- 但是对象A不会被dealloc因为对象B强引用了它
- …...

这样的话，这两个对象就会一直在内存中尽管它们“应该”被回收掉。

所以，我们要担心的是循环引用而不是block，像下面这种情况不会产生循环就没有问题：

```objc
[myArray enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop){
   [self doSomethingWithObject:obj];
}];
```

Block retain了self，但是self并没有引用block，如果其中一个被释放了，不会有循环引用产生而且所有的对象都会及时得到释放

下面这种情况就会有问题：

```objc
//In the interface:
@property (strong) void(^myBlock)(id obj, NSUInteger idx, BOOL *stop);

//In the implementation:
[self setMyBlock:^(id obj, NSUInteger idx, BOOL *stop) {
  [self doSomethingWithObj:obj];     
}];
```

现在，self对block有一个强引用，而且block对self也有一个强引用，这样就产生了一个循环。。解决这个问题也很简单，将block对self的引用改为弱引用：

```objc
__weak MyObject *weakSelf = self;
[self setMyBlock:^(id obj, NSUInteger idx, BOOL *stop) {
  [weakSelf doSomethingWithObj:obj];     
}];
```

