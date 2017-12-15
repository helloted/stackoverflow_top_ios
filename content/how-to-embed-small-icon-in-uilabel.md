# UILabel嵌入小图片
[How to embed small icon in UILabel](https://stackoverflow.com/questions/19318421/how-to-embed-small-icon-in-uilabel)

___



> 1

**Swift Version**

```swift
//Create Attachment
    let imageAttachment =  NSTextAttachment()
    imageAttachment.image = UIImage(named:"iPhoneIcon")
    //Set bound to reposition
    let imageOffsetY:CGFloat = -5.0;
    imageAttachment.bounds = CGRect(x: 0, y: imageOffsetY, width: imageAttachment.image!.size.width, height: imageAttachment.image!.size.height)
    //Create string with attachment
    let attachmentString = NSAttributedString(attachment: imageAttachment)
    //Initialize mutable string
    let completeText = NSMutableAttributedString(string: "")
    //Add image to mutable string
    completeText.append(attachmentString)
    //Add your text to mutable string
    let  textAfterIcon = NSMutableAttributedString(string: "Using attachment.bounds!")
    completeText.append(textAfterIcon)
    self.mobileLabel.textAlignment = .center;
    self.mobileLabel.attributedText = completeText;
```

------

**Objective-C Version**

```objc
 NSTextAttachment *imageAttachment = [[NSTextAttachment alloc] init];
imageAttachment.image = [UIImage imageNamed:@"iPhoneIcon"];
CGFloat imageOffsetY = -5.0;
imageAttachment.bounds = CGRectMake(0, imageOffsetY, imageAttachment.image.size.width, imageAttachment.image.size.height);
NSAttributedString *attachmentString = [NSAttributedString attributedStringWithAttachment:imageAttachment];
NSMutableAttributedString *completeText= [[NSMutableAttributedString alloc] initWithString:@""];
[completeText appendAttributedString:attachmentString];
NSMutableAttributedString *textAfterIcon= [[NSMutableAttributedString alloc] initWithString:@"Using attachment.bounds!"];
[completeText appendAttributedString:textAfterIcon];
self.mobileLabel.textAlignment=NSTextAlignmentRight;
self.mobileLabel.attributedText=completeText;]
```

用 **attachment.bounds**来居中图片

![img](/images/08.png)

