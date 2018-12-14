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

8、旋转

```c++
[myView setTransform:CGAffineTransformMakeRotation(-M_PI / 2)];
```

9、KVO的keypath

```
#define KVOKeyPath(PATH)  @(((void)(NO && ((void)PATH, NO)), strchr(# PATH, '.') + 1))
```

(void)是为了防止逗号表达式的warning。加NO是为了C短路判断条件表达式。编译器看见了NO && 以后，就会很快的跳过之后的判断条件。

在宏中，#代表把宏的参数名转化为一个字符串。而strchr函数使用来查找字符串s中首次出现字符c的位置。返回首次出现字符c的位置的指针，返回的地址是被查找字符串指针开始的第一个与字符c相同字符的指针，如果字符串中不存在字符c则返回NULL。

最后我们通过strchr函数得到了一个C的字符串，通过@( )包起来，就变成了一个OC的字符串了。