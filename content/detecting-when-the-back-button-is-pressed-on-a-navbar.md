# 监测NavBar的返回按钮被点击
[Detecting when the 'back' button is pressed on a navbar](https://stackoverflow.com/questions/8228411/detecting-when-the-back-button-is-pressed-on-a-navbar)

___



> 1

 iOS 5之后用这个方法很方便

 `- (BOOL)isMovingFromParentViewController`:

```
- (void)viewWillDisappear:(BOOL)animated {
  [super viewWillDisappear:animated];

  if (self.isMovingFromParentViewController) {
    // Do your stuff here
  }
}
```

`- (BOOL)isMovingFromParentViewController` 返回YES就是在pop出去

如果是 presenting modal view controllers 应该用 `- (BOOL)isBeingDismissed` :

```
- (void)viewWillDisappear:(BOOL)animated {
  [super viewWillDisappear:animated];

  if (self.isBeingDismissed) {
    // Do your stuff here
  }
}
```

综上可以，这样判断

```
- (void)viewWillDisappear:(BOOL)animated {
  [super viewWillDisappear:animated];

  if (self.isMovingFromParentViewController || self.isBeingDismissed) {
    // 这里是返回上一个界面
  }
}
```