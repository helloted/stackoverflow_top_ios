# UILabel文字垂直居上？
https://stackoverflow.com/questions/1054558/vertically-align-text-to-top-within-a-uilabel

___



> 1

UIKit自带的功能是没有办法让垂直居上的，但是可以通过`[myLabel sizeToFit];`来达到类似效果

![img](/images/01.png)

如果数量超过一行

```objc
   myLabel.numberOfLines = 0;
    [myLabel sizeToFit];
```

![img](/images/02.png)

___



> 2

把UILabel换成UITextView可以达到这个效果。如果你换成UITextView，你可以通过禁用交互关闭ScrollView属性，这样效果看起来更新UILabel

___

> 3

写UIlabel的子类

```
@interface MFTopAlignedLabel : UILabel

@end


@implementation MFTopAlignedLabel

- (void)drawTextInRect:(CGRect) rect
{
    NSAttributedString *attributedText = [[NSAttributedString alloc]     initWithString:self.text attributes:@{NSFontAttributeName:self.font}];
    rect.size.height = [attributedText boundingRectWithSize:rect.size
                                            options:NSStringDrawingUsesLineFragmentOrigin
                                            context:nil].size.height;
    if (self.numberOfLines != 0) {
        rect.size.height = MIN(rect.size.height, self.numberOfLines * self.font.lineHeight);
    }
    [super drawTextInRect:rect];
}

@end
```