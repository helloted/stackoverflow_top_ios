# 去除UIButton修改标题时的动画效果

[How to stop unwanted UIButton animation on title change?](https://stackoverflow.com/questions/18946490/how-to-stop-unwanted-uibutton-animation-on-title-change)

___



> 1

```objc
[UIView setAnimationsEnabled:NO];
[_button setTitle:@"title" forState:UIControlStateNormal];
[UIView setAnimationsEnabled:YES];
```

如果是系统的button，你需要在重新启用动画前调用

```objc
[_button layoutIfNeeded];
```

> 2

```objc
[UIView performWithoutAnimation:^{
  [self.myButton setTitle:text forState:UIControlStateNormal];
  [self.myButton layoutIfNeeded];
}];
```