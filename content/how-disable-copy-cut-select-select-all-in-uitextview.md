# 禁用UITextView的粘贴板功能
[How disable Copy, Cut, Select, Select All in UITextView](https://stackoverflow.com/questions/1426731/how-disable-copy-cut-select-select-all-in-uitextview)

___



> 1

禁用粘贴板功能很简单，定义一个 `UITextView` 的子类重写 `canPerformAction:withSender:` 返回 `NO` :

```objc
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender
{
    if (action == @selector(paste:))
        return NO;
    return [super canPerformAction:action withSender:sender];
}
```