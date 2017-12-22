# 字符串常量作为key
[Using a constant NSString as the key for NSUserDefaults](https://stackoverflow.com/questions/753755/using-a-constant-nsstring-as-the-key-for-nsuserdefaults)

___



> 1

应该使用

```
NSString * const kPolygonNumberOfSides = @"..."; // 一个常量指针指向一个NSString
```

而不是

```
NSString const * kPolygonNumberOfSides = @"..."; // 一个指针指向常量相当于，const NSString *
```

第一个是一个常量指针指向一个字符串对象，不变的是指针。

第二个是一个指针指向常量字符串，不变的是这个字符串。

有一点细微的区别，当使用

```
- (void)setObject:(id)value forKey:(NSString *)defaultName;
```

defaultName参数需要的是一个NSString *类型，当你传递的是一个指针(变量)，会报Waring

另外，我需要指出用这些常量最好加上关键字static如果他们只是在一个文件内使用。因为如果你不声明为一个static，它们会作为一个全局命名变量，你在其他文件内不能使用相同名字的变量。所以最好是这样声明：

```
static NSString * const kSomeLabel = @"...";
```