# atomic和nonatomic有什么区别？
[What's the difference between the atomic and nonatomic attributes?](https://stackoverflow.com/questions/588866/whats-the-difference-between-the-atomic-and-nonatomic-attributes)

> 1

使用atomic，`synthesized setter/getter `将会确保整个属性总是会从getter中取值或者从setter去赋值，不管其他线程的赋值操作。就是说，如果线程A在取值getter的时候，线程B调用了setter赋值操作，一个实际可用的值--一个autoreleased对象—将会返回在A线程。也就是说有互斥。

使用nonatomic的时候，没有上面这种保证，所以，nonatomic被认为比atomic更快

atomic并没有确保线程安全，如果线程A在调用getter取值的同时线程B和线程C在调用setter赋值不同的值，线程A有可能得到三个值中的任何一个：之前赋值或者BC线程赋的值，没有办法知道是哪个值。

确保数据完整性—多线程编程的一个主要挑战—是用过其他手段来实现的。

附加：

一个属性的atomicity同样无法确保线程安全当需要依赖多个属性时。

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

Basically, the atomic version has to take a lock in order to guarantee thread safety, and also is bumping the ref count on the object (and the autorelease count to balance it) so that the object is guaranteed to exist for the caller, otherwise there is a potential race condition if another thread is setting the value, causing the ref count to drop to 0.

There are actually a large number of different variants of how these things work depending on whether the properties are scalar values or objects, and how retain, copy, readonly, nonatomic, etc interact. In general the property synthesizers just know how to do the "right thing" for all combinations.

一般来说，atomic有设置互斥锁来保证线程安全，并且还要对象的引用计数+1(并且自动释放计数来平衡)，这样才能保证调用者能够获得对象，否则另外一个线程在设置这个值得时候可能会使引用计数归为0。

实际上会有许多变种，取决于属性值或者对象是retain, copy, readonly, nonatomic。一般来说，针对这些可能性，synthesizers会做出正确的事。