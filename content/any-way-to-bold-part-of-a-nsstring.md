# 字符串部分粗体
[Any way to bold part of a NSString?](https://stackoverflow.com/questions/6013705/any-way-to-bold-part-of-a-nsstring)

___



> 1

用NSMutableAttributedString

```objc
NSMutableAttributedString *string = [[NSMutableAttributedString alloc] initWithString:@"Approximate Distance: 120m away"];
NSRange selectedRange = NSMakeRange(22, 4); // 4 characters, starting at index 22

[string beginEditing];

[string addAttribute:NSFontAttributeName
           value:[NSFont fontWithName:@"Helvetica-Bold" size:12.0]
           range:selectedRange];

[string endEditing];
```

