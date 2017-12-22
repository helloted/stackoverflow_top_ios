# UIAlertController自定义字体
[UIAlertController custom font, size, color](https://stackoverflow.com/questions/26460706/uialertcontroller-custom-font-size-color)

___



> 1

不确定是否与私有API属性有冲突，iOS 8 用KVC可以实现

```objc
UIAlertController *alertVC = [UIAlertController alertControllerWithTitle:@"Dont care what goes here, since we're about to change below" message:@"" preferredStyle:UIAlertControllerStyleActionSheet];
NSMutableAttributedString *hogan = [[NSMutableAttributedString alloc] initWithString:@"Presenting the great... Hulk Hogan!"];
[hogan addAttribute:NSFontAttributeName
              value:[UIFont systemFontOfSize:50.0]
              range:NSMakeRange(24, 11)];
[alertVC setValue:hogan forKey:@"attributedTitle"];



UIAlertAction *button = [UIAlertAction actionWithTitle:@"Label text" 
                                        style:UIAlertActionStyleDefault
                                        handler:^(UIAlertAction *action){
                                                    //add code to make something happen once tapped
}];
UIImage *accessoryImage = [UIImage imageNamed:@"someImage"];
[button setValue:accessoryImage forKey:@"image"];
```

Swift:

```swift
let alert = UIAlertController(title: nil, message: nil, preferredStyle: .ActionSheet)

let action = UIAlertAction(title: "Some title", style: .Default, handler: nil)
let attributedText = NSMutableAttributedString(string: "Some title")

let range = NSRange(location: 0, length: attributedText.length)
attributedText.addAttribute(NSKernAttributeName, value: 1.5, range: range)
attributedText.addAttribute(NSFontAttributeName, value: UIFont(name: "ProximaNova-Semibold", size: 20.0)!, range: range)

alert.addAction(action)

presentViewController(alert, animated: true, completion: nil)

// this has to be set after presenting the alert, otherwise the internal property __representer is nil
guard let label = action.valueForKey("__representer")?.valueForKey("label") as? UILabel else { return }
label.attributedText = attributedText
```