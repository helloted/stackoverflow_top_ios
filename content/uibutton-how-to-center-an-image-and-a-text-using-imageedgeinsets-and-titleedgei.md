# 如何使UIButton的图片和文字都居中？
[UIButton: how to center an image and a text using imageEdgeInsets and titleEdgeInsets?](https://stackoverflow.com/questions/2451223/uibutton-how-to-center-an-image-and-a-text-using-imageedgeinsets-and-titleedgei)

___



> 1

#### iOS6及以下用以下代码

```Objc
// 图片与文字之间的距离
CGFloat spacing = 6.0;

// 把文字放低和居左可以文字在图片下面
CGSize imageSize = button.imageView.frame.size;
button.titleEdgeInsets = UIEdgeInsetsMake(
  0.0, - imageSize.width, - (imageSize.height + spacing), 0.0);

// 把图片放上和居右可以让图片在文字上面
CGSize titleSize = button.titleLabel.frame.size;
button.imageEdgeInsets = UIEdgeInsetsMake(
  - (titleSize.height + spacing), 0.0, 0.0, - titleSize.width);
```

#### iOS 7+

```objc
// the space between the image and text
CGFloat spacing = 6.0;

// lower the text and push it left so it appears centered 
//  below the image
CGSize imageSize = button.imageView.image.size;
button.titleEdgeInsets = UIEdgeInsetsMake(
  0.0, - imageSize.width, - (imageSize.height + spacing), 0.0);

// raise the image and push it right so it appears centered
//  above the text
CGSize titleSize = [button.titleLabel.text sizeWithAttributes:@{NSFontAttributeName: button.titleLabel.font}];
button.imageEdgeInsets = UIEdgeInsetsMake(
  - (titleSize.height + spacing), 0.0, 0.0, - titleSize.width);

// increase the content height to avoid clipping
CGFloat edgeOffset = fabsf(titleSize.height - imageSize.height) / 2.0;
button.contentEdgeInsets = UIEdgeInsetsMake(edgeOffset, 0.0, edgeOffset, 0.0);
```

#### Swift

```swift
extension UIButton {
  func alignVertical(spacing: CGFloat = 6.0) {
    guard let imageSize = self.imageView?.image?.size,
      let text = self.titleLabel?.text,
      let font = self.titleLabel?.font
      else { return }
    self.titleEdgeInsets = UIEdgeInsets(top: 0.0, left: -imageSize.width, bottom: -(imageSize.height + spacing), right: 0.0)
    let labelString = NSString(string: text)
    let titleSize = labelString.size(attributes: [NSFontAttributeName: font])
    self.imageEdgeInsets = UIEdgeInsets(top: -(titleSize.height + spacing), left: 0.0, bottom: 0.0, right: -titleSize.width)
    let edgeOffset = abs(titleSize.height - imageSize.height) / 2.0;
    self.contentEdgeInsets = UIEdgeInsets(top: edgeOffset, left: 0.0, bottom: edgeOffset, right: 0.0)
  }
}
```