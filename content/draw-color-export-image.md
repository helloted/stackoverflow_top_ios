# 画图并导出沙盒
___



> 1

```objc
    UIImage * image = [UIImage imageNamed:@"01.png"];
    CGSize size = CGSizeMake(1024, 1024);
    UIGraphicsBeginImageContext(size);
    CGContextRef context = UIGraphicsGetCurrentContext();
    CGContextSetFillColorWithColor(context, [RGBFromHex(0x0FBEEC) CGColor]);
    CGContextFillRect(context, CGRectMake(0, 0, 1024, 1024));
    
    [image drawInRect:CGRectMake(0, 0, size.width, size.height)];
    UIImage *resultingImage =UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,NSUserDomainMask, YES);
    NSString *filePath = [[paths objectAtIndex:0] stringByAppendingPathComponent:@"new.png"]; // 保存文件的名称
    BOOL result = [UIImagePNGRepresentation(resultingImage) writeToFile: filePath atomically:YES];
```