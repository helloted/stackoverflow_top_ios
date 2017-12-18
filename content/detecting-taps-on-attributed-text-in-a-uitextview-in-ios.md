# 检测UITextView上的点击了字符串
[Detecting taps on attributed text in a UITextView in iOS](https://stackoverflow.com/questions/19332283/detecting-taps-on-attributed-text-in-a-uitextview-in-ios)

___



> 1

1、自定义一个attributed string

```Objc
NSAttributedString* attributedString = [[NSAttributedString alloc] initWithString:@"a clickable word" attributes:@{ @"myCustomTag" : @(YES) }];
[paragraph appendAttributedString:attributedString];
```

2、创建一个UITextView来显示字符串，并且在上面加上手势

```objc
- (void)textTapped:(UITapGestureRecognizer *)recognizer
{
    UITextView *textView = (UITextView *)recognizer.view;

    // 定位点击的坐标位置
    NSLayoutManager *layoutManager = textView.layoutManager;
    CGPoint location = [recognizer locationInView:textView];
    location.x -= textView.textContainerInset.left;
    location.y -= textView.textContainerInset.top;

    // 找到哪些字符串被点击了
    NSUInteger characterIndex;
    characterIndex = [layoutManager characterIndexForPoint:location
                                           inTextContainer:textView.textContainer
                  fractionOfDistanceBetweenInsertionPoints:NULL];

    if (characterIndex < textView.textStorage.length) {

        NSRange range;
        id value = [textView.attributedText attribute:@"myCustomTag" atIndex:characterIndex effectiveRange:&range];

        // 要做的操作

        NSLog(@"%@, %d, %d", value, range.location, range.length);
    }
}
```

