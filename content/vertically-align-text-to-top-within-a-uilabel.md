# UILabel文字垂直居上？
https://stackoverflow.com/questions/1054558/vertically-align-text-to-top-within-a-uilabel

___



> 1

UIKit自带的功能是没有办法让垂直居上的，但是可以通过`[myLabel sizeToFit];`来达到类似效果

![img](/images/01.png)

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