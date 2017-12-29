# 一行代码了事
___

1、当前选中的UITableView Index:

```objc
NSIndexPath *selectedIndexPath = [tableView indexPathForSelectedRow];
```

2、检测当前键盘是否弹出？

```
BOOL isFisrt =  [myTextField isFirstResponder]
```

3、移除字符串空格

```
NSString *stringWithoutSpaces = [myString stringByReplacingOccurrencesOfString:@" " withString:@""];
```

4、最顶层加一个View

```
[[[UIApplication sharedApplication] keyWindow] addSubview:someView]
```

5、字典拼接

```
[NSMutableDictionary addEntriesFromDictionary:otherDict]
```

6、获取毫秒时间戳

```
CFAbsoluteTime timeInSeconds = CFAbsoluteTimeGetCurrent();
```

7、模拟器沙盒路径

```
po NSHomeDirectory();
```

