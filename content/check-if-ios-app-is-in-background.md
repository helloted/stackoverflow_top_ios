# 检测iOS APP是否在后台
[Check if iOS app is in background](https://stackoverflow.com/questions/5835806/check-if-ios-app-is-in-background)

___



> 1

App delegate会回调来显示状态改变，你可以利用这个来进行跟踪

同样，UIApplication的属性[applicationState](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplication_Class/#//apple_ref/occ/instp/UIApplication/applicationState) 也可以知道状态。

```objc
[[UIApplication sharedApplication] applicationState]
```

```objc
typedef NS_ENUM(NSInteger, UIApplicationState) {
    UIApplicationStateActive,
    UIApplicationStateInactive,
    UIApplicationStateBackground
} NS_ENUM_AVAILABLE_IOS(4_0);
```

