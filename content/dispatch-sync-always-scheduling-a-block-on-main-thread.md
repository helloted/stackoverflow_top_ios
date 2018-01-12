# Dispatch_sync
[dispatch_sync always scheduling a block on Main Thread](https://stackoverflow.com/questions/13972048/dispatch-sync-always-scheduling-a-block-on-main-thread)

```
  dispatch_sync(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{

        if ([NSThread isMainThread]) {
            NSLog(@"Main Thread");
        }
        else
            NSLog(@"Not on Main Thread");

        //Some Process
    });
```

打印结果是Main Thread

___



> 1

苹果官方文档[dispatch_sync](https://developer.apple.com/documentation/dispatch/1452870-dispatch_sync?language=objc)

> Submits a block to a dispatch queue for synchronous execution. Unlike [`dispatch_async`](https://developer.apple.com/documentation/dispatch/1453057-dispatch_async?language=objc), this function does not return until the block has finished. Calling this function and targeting the current queue results in deadlock.
>
> Unlike with `dispatch_async`, no retain is performed on the target queue. Because calls to this function are synchronous, it "borrows" the reference of the caller. Moreover, no `Block_copy` is performed on the block.
>
> As an optimization, this function invokes the block on the current thread when possible.

调用dispatch_sync在当前队列会导致死锁。另外，最优化处理，dispatch_sync在在当前线程上执行block

> 2

```objc
        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            dispatch_sync(dispatch_get_main_queue(), ^{
                NSLog(@"is main thread? %i", (int)[NSThread isMainThread]);
            });
        });
        
        dispatch_main();
```

打印内容为非主线程。