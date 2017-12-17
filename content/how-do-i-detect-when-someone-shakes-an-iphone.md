# 如何检测手机的摇动？
[How do I detect when someone shakes an iPhone?](https://stackoverflow.com/questions/150446/how-do-i-detect-when-someone-shakes-an-iphone)

___



> 1

主要诀窍是你得有一个View（不是UIViewController）来成为firstResponder接收摇动事件的信息：

```objc
@implementation ShakingView

- (void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event
{
    if ( event.subtype == UIEventSubtypeMotionShake )
    {
        // Put in code here to handle shake
    }

    if ( [super respondsToSelector:@selector(motionEnded:withEvent:)] )
        [super motionEnded:motion withEvent:event];
}

- (BOOL)canBecomeFirstResponder
{ return YES; }

@end
```

在View Controller，你需要设置这个shakeView成为firstResponder

```objc
- (void) viewWillAppear:(BOOL)animated
{
    [shakeView becomeFirstResponder];
    [super viewWillAppear:animated];
}
- (void) viewWillDisappear:(BOOL)animated
{
    [shakeView resignFirstResponder];
    [super viewWillDisappear:animated];
}
```

不要忘了，如果你有其他的View有可能成为第一响应者(比如搜索框或者文字输入框),你应该重新设置shakingView成为第一响应者当其他View完成后。