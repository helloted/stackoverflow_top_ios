# APP里如何使用自定义字体？
[Can I embed a custom font in an iPhone application?](https://stackoverflow.com/questions/360751/can-i-embed-a-custom-font-in-an-iphone-application)

___



> 1

iOS3.2之后就已经支持自定义字体，这是官方文档

**Custom Font Support**
Applications that want to use custom fonts can now include those fonts in their application bundle and register those fonts with the system by including the UIAppFonts key in their Info.plist file. The value of this key is an array of strings identifying the font files in the application’s bundle. When the system sees the key, it loads the specified fonts and makes them available to the application.

一旦字体在 `Info.plist`里被设置，你就可以使用了

1. 将你的自定义字体文件作为资源文件添加进项目中
2.  `Info.plist` 添加一个item，Key是 `UIAppFonts`.
3. 让这个item是一个Array类型
4. 将你的字体名字(包含后缀名)，填入到Array里面
5. 在代码里可以这样调用你的自定义字体 `[UIFont fontWithName:@"CustomFontName" size:12]`

