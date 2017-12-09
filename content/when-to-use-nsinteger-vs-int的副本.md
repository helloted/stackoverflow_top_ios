# 更改布局时如何用动画？
[How do I animate constraint changes?](https://stackoverflow.com/questions/12622424/how-do-i-animate-constraint-changes)

问题：

```
- (void)moveBannerOffScreen {
    [UIView animateWithDuration:5
             animations:^{
                          _addBannerDistanceFromBottomConstraint.constant = -32;
                     }];
    bannerIsVisible = FALSE;
}

- (void)moveBannerOnScreen {
    [UIView animateWithDuration:5
             animations:^{
                         _addBannerDistanceFromBottomConstraint.constant = 0;
             }];
    bannerIsVisible = TRUE;
}
```

以上代码，可以变更布局，但是变更的时候没有动画，如何才能有动画呢？

___



> 1

两个重点

1. 在animation block之前你需要调用 `layoutIfNeeded` ，苹果建议在动画block之前调用这个方法以确保所有的布局依赖都已经建立完成 。
2. 你需要对 **parent view** (e.g. `self.view`)操作而不是子View。这样的化，就会更新所有的布局，包括其他动画变更有改变的布局。

```objc
- (void)moveBannerOffScreen {
    [self.view layoutIfNeeded];

    _addBannerDistanceFromBottomConstraint.constant = -32;
    [UIView animateWithDuration:5
        animations:^{
            [self.view layoutIfNeeded]; // Called on parent view
        }];
    bannerIsVisible = FALSE;
}

- (void)moveBannerOnScreen { 
    [self.view layoutIfNeeded];

    _addBannerDistanceFromBottomConstraint.constant = 0;
    [UIView animateWithDuration:5
        animations:^{
            [self.view layoutIfNeeded]; // Called on parent view
        }];
    bannerIsVisible = TRUE;
}
```

