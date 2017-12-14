# performSelector: vs. method
[Using -performSelector: vs. just calling the method](https://stackoverflow.com/questions/1493125/using-performselector-vs-just-calling-the-method)

```
[object performSelector:@selector(doSomething)]; 
[object doSomething];
```

有什么区别？

___



> 1

一般来说，performSelector允许你动态检测哪个selector给对象进行调用，换句话说，在运行时之前，selector不会被检测。而不像Method在编译的时候就会被检测是否合适

下面这种情况两者是相同的：

```
[anObject aMethod]; 
[anObject performSelector:@selector(aMethod)]; 
```

performSelector允许你这样做:

```objc
SEL aSelector = findTheAppropriateSelectorForTheCurrentSituation(); //找到合适的selector
[anObject performSelector: aSelector];
```

另外可以用performSelector调用不能显式调用的方法

```objc
SEL aSelector = NSSelecotrFromString(@"dealloc"); //dealloc不能被显式调用
[anObject performSelector: aSelector];
```

