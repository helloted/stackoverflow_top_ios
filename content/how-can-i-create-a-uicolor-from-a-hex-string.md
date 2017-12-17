# 16进制的UIColor
[How can I create a UIColor from a hex string?](https://stackoverflow.com/questions/1560081/how-can-i-create-a-uicolor-from-a-hex-string)

___



> 1

可以通过这种方式

```objc
#define UIColorFromRGB(rgbValue) \
[UIColor colorWithRed:((float)((rgbValue & 0xFF0000) >> 16))/255.0 \
                green:((float)((rgbValue & 0x00FF00) >>  8))/255.0 \
                 blue:((float)((rgbValue & 0x0000FF) >>  0))/255.0 \
                alpha:1.0]
```

```objc
label.textColor = UIColorFromRGB(0xBC1128);
```

