# NSArray的深拷贝
[Deep copying an NSArray](https://stackoverflow.com/questions/647260/deep-copying-an-nsarray)

___



> 1

#### 默认的copy会对NSArray进行浅拷贝

因为调用 `copy` 其实就是调用 `copyWithZone:NULL` 进行拷贝默认的空间.  `copy` 不会进行深拷贝.不可变对象只会给一个浅拷贝

- [immutableObject copy] // 浅复制
- [immutableObject mutableCopy] //单层深复制 //NSArray层级的深复制
- [mutableObject copy] //单层深复制
- [mutableObject mutableCopy] //单层深复制

#### initWithArray:CopyItems: 单层深拷贝

```
NSArray *deepCopyArray = [[NSArray alloc] initWithArray:someArray copyItems:YES];
```

#### `NSCoding`进行真正的深拷贝

```
NSArray *trueDeepCopyArray = [NSKeyedUnarchiver unarchiveObjectWithData:[NSKeyedArchiver archivedDataWithRootObject:oldArray]];
```

这种拷贝可以对数组里面的元素也进行深拷贝。

参考苹果官方文档[集合类拷贝](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Collections/Articles/Copying.html#//apple_ref/doc/uid/TP40010162-SW1)