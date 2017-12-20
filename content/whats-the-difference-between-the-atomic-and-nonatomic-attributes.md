# atomic和nonatomic有什么区别？
[What's the difference between the atomic and nonatomic attributes?](https://stackoverflow.com/questions/588866/whats-the-difference-between-the-atomic-and-nonatomic-attributes)

___



> 1

使用atomic，`synthesized setter/getter `将会确保整个属性总是会从getter中取值或者从setter去赋值，不管其他线程的赋值操作。就是说，如果线程A在取值getter的时候，线程B调用了setter赋值操作，一个实际可用的值--一个autoreleased对象—将会返回在A线程。也就是说有互斥。

使用nonatomic的时候，没有上面这种保证，所以，nonatomic被认为比atomic更快

atomic并没有确保线程安全，如果线程A在调用getter取值的同时线程B和线程C在调用setter赋值不同的值，线程A有可能得到三个值中的任何一个：之前赋值或者BC线程赋的值，没有办法知道是哪个值。

确保数据完整性—多线程编程的一个主要挑战—是用过其他手段来实现的。

附加：

一个属性的atomicity同样无法确保线程安全当需要依赖多个属性时。

[苹果官方文档举例](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html#//apple_ref/doc/uid/TP40011210-CH5-SW1)

> **Note:** Property atomicity is not synonymous with an object’s *thread safety*.Consider an `XYZPerson` object in which both a person’s first and last names are changed using atomic accessors from one thread. If another thread accesses both names at the same time, the atomic getter methods will return complete strings (without crashing), but there’s no guarantee that those values will be the right names relative to each other. If the first name is accessed before the change, but the last name is accessed after the change, you’ll end up with an inconsistent, mismatched pair of names.This example is quite simple, but the problem of thread safety becomes much more complex when considered across a network of related objects. Thread safety is covered in more detail in *Concurrency Programming Guide*.

如果fullName=firstName+lastName；则不能保证fullName的线性安全。

___



> 2

```
//@property(nonatomic, retain) UITextField *userName;
//Generates roughly

- (UITextField *) userName {
    return userName;
}

- (void) setUserName:(UITextField *)userName_ {
    [userName_ retain];
    [userName release];
    userName = userName_;
}
```

atomic会更复杂一些

```
//@property(retain) UITextField *userName;
//Generates roughly

- (UITextField *) userName {
    UITextField *retval = nil;
    @synchronized(self) {
        retval = [[userName retain] autorelease];
    }
    return retval;
}

- (void) setUserName:(UITextField *)userName_ {
    @synchronized(self) {
      [userName_ retain];
      [userName release];
      userName = userName_;
    }
}
```

一般来说，atomic有设置互斥锁来保证线程安全，并且还要对象的引用计数+1(并且自动释放计数来平衡)，这样才能保证调用者能够获得对象，否则另外一个线程在设置这个值得时候可能会使引用计数归为0。

实际上会有许多变种，取决于属性值或者对象是retain, copy, readonly, nonatomic。一般来说，针对这些可能性，synthesizers会做出正确的事。