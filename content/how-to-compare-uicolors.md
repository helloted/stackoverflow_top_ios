# UIColor进行比较
[How to compare UIColors?](https://stackoverflow.com/questions/970475/how-to-compare-uicolors)

___



> 1

`isEqual:` 会返回 `NO` 如果比较的两个颜色是不同的类型 (比如 `#FFF` 和 `[UIColor whiteColor]`)，所以用下面这方法来比较

```objc
- (BOOL)isEqualToColor:(UIColor *)otherColor {
    CGColorSpaceRef colorSpaceRGB = CGColorSpaceCreateDeviceRGB();

    UIColor *(^convertColorToRGBSpace)(UIColor*) = ^(UIColor *color) {
        if (CGColorSpaceGetModel(CGColorGetColorSpace(color.CGColor)) == kCGColorSpaceModelMonochrome) {
            const CGFloat *oldComponents = CGColorGetComponents(color.CGColor);
            CGFloat components[4] = {oldComponents[0], oldComponents[0], oldComponents[0], oldComponents[1]};
            CGColorRef colorRef = CGColorCreate( colorSpaceRGB, components );

            UIColor *color = [UIColor colorWithCGColor:colorRef];
            CGColorRelease(colorRef);
            return color;            
        } else
            return color;
    };

    UIColor *selfColor = convertColorToRGBSpace(self);
    otherColor = convertColorToRGBSpace(otherColor);
    CGColorSpaceRelease(colorSpaceRGB);

    return [selfColor isEqual:otherColor];
}
```

