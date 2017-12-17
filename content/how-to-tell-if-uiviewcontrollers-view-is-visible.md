# 如何判断UIViewController的View是否可见
[How to tell if UIViewController's view is visible](https://stackoverflow.com/questions/2777438/how-to-tell-if-uiviewcontrollers-view-is-visible)

___



> 1

View的 [window property](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW55) 非空则表示这个View可见。

另外，调用View的方法会导致View进行Load（如果之前没有load的话），这是没有必要的而且可能会导致未知情况，所以最好在调用方法之前先确认一下是否已经被load了

#### Objective-C:

```
if (viewController.isViewLoaded && viewController.view.window) {
    // viewController is visible
}
```

如果你有一个UINavigationController来管理view controllers, 那你应该通过检测这个 [visibleViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UINavigationController_Class/Reference/Reference.html#//apple_ref/doc/uid/TP40006934-CH3-SW1) 属性.

#### Swift

```
if viewController.viewIfLoaded?.window != nil {
    // viewController is visible
}
```