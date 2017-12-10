# 创建一个带模糊效果的View
[Creating a blurring overlay view](https://stackoverflow.com/questions/17041669/creating-a-blurring-overlay-view)

如何达到以下效果？

![img](/images/06.jpg)

___



> 1

你可以用 `UIVisualEffectView` 来达到这个效果. 这是个原生API可以达到很好的效果和省电，也容易声明：

**Swift:**

```swift
//only apply the blur if the user hasn't disabled transparency effects
if !UIAccessibilityIsReduceTransparencyEnabled() {
    view.backgroundColor = .clear

    let blurEffect = UIBlurEffect(style: .dark)
    let blurEffectView = UIVisualEffectView(effect: blurEffect)
    //always fill the view
    blurEffectView.frame = self.view.bounds
    blurEffectView.autoresizingMask = [.flexibleWidth, .flexibleHeight]

    view.addSubview(blurEffectView) //if you have more UIViews, use an insertSubview API to place it where needed
} else {
    view.backgroundColor = .black
}
```

**Objective-C:**

```objc
//only apply the blur if the user hasn't disabled transparency effects
if (!UIAccessibilityIsReduceTransparencyEnabled()) {
    self.view.backgroundColor = [UIColor clearColor];

    UIBlurEffect *blurEffect = [UIBlurEffect effectWithStyle:UIBlurEffectStyleDark];
    UIVisualEffectView *blurEffectView = [[UIVisualEffectView alloc] initWithEffect:blurEffect];
    //always fill the view
    blurEffectView.frame = self.view.bounds;
    blurEffectView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;

    [self.view addSubview:blurEffectView]; //if you have more UIViews, use an insertSubview API to place it where needed
} else {
    self.view.backgroundColor = [UIColor blackColor];
}
```

另外，如果你是要presenting这个Viewcontroller来模糊遮挡底下的内容，你需要设置 modal presentation style 成 Over Current Context，并且背景颜色也要设置为空白来保证底下的内容依旧可见。