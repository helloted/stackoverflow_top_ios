# 如何隐藏UINavigationBar底部的线？
[How to hide UINavigationBar 1px bottom line](https://stackoverflow.com/questions/19226965/how-to-hide-uinavigationbar-1px-bottom-line)

___



> 1

以下代码可以有全局效果

```objc
[[UINavigationBar appearance] setBackgroundImage:[[UIImage alloc] init]
                                  forBarPosition:UIBarPositionAny
                                      barMetrics:UIBarMetricsDefault];

[[UINavigationBar appearance] setShadowImage:[[UIImage alloc] init]];
```

![img](/images/05.png)