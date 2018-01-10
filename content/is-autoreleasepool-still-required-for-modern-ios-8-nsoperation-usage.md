# NSOperation或者GCD编程是否需要autoreleasepool？
[Is @autoreleasepool still required for modern iOS 8 NSOperation usage?](https://stackoverflow.com/questions/24562043/is-autoreleasepool-still-required-for-modern-ios-8-nsoperation-usage)

___



> 1

如果你正在使用 `NSOperation` 并且声明了 `main` 方法, 不需要去创建一个autoreleasepool.  `start` 方法会默认 pushes一个 `NSAutoReleasePool`, 调用 `main` 随后会 pops `NSAutoReleasePool`.  `NSInvocationOperation` 和 `NSBlockOperation`也一样， `start` 方法的声明是一样的.

下面是 `NSOperation`的 `start` 方法的一些操作，注意调用了 NSPushAutoreleasePool, 随后调用main 方法，接着调用NSPopAutoreleasePool:

```Objc
Foundation`-[newMyObj__NSOperationInternal _start:]:
0x7fff8e5df30f:  pushq  %rbp

...

0x7fff8e5df49c:  callq  *-0x16b95bb2(%rip)        ; (void *)0x00007fff8d9d30c0: objc_msgSend
0x7fff8e5df4a2:  movl   $0x1, %edi

; new NSAutoreleasePool is pushed here
0x7fff8e5df4a7:  callq  0x7fff8e5df6d6            ; NSPushAutoreleasePool

... NSOperation main is called

0x7fff8e5df6a4:  callq  *-0x16b95dba(%rip)        ; (void *)0x00007fff8d9d30c0: objc_msgSend
0x7fff8e5df6aa:  movq   %r15, %rdi

; new NSAutoreleasePool is popped here, which releases any objects added in the main method
0x7fff8e5df6ad:  callq  0x7fff8e5e1408            ; NSPopAutoreleasePool
```

![img](/images/15.png)

```objc
#import <Foundation/Foundation.h>

@interface MyObj : NSObject
@end

@implementation MyObj

- (void)dealloc {
    NSLog(@"dealloc");
}

@end

@interface TestOp : NSOperation {
    MyObj *obj;
}

@end

@implementation TestOp

- (MyObj *)setMyObj:(MyObj *)o {
    MyObj *old = obj;
    obj = o;
    return old;
}

- (void)main {
    MyObj *old = [self setMyObj:[MyObj new]];
    [self setMyObj:old];
}

@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        NSLog(@"Hello, World!");

        NSOperationQueue *q = [NSOperationQueue new];
        TestOp *op = [TestOp new];
        [q addOperation:op];

        [op waitUntilFinished];
    }
    return 0;
}
```

GCD也有类似的管理[Concurrency Programming Guide](https://developer.apple.com/library/ios/documentation/General/Conceptual/ConcurrencyProgrammingGuide/OperationQueues/OperationQueues.html#//apple_ref/doc/uid/TP40008091-CH102-SW17):

如果您的Block创建了多个Objective-C对象，则可能需要将block的部分代码放在@autorelease块中，以处理这些对象的内存管理。虽然GCD调度队列有他们自己的autorelease池，他们不保证什么时候这些池被drained。如果您的应用程序受到内存限制，创建您自己的自动释放池允许您以更有规律的间隔释放自动释放对象的内存。

