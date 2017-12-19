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

5、判断一个时间在另外两个时间之间？

```
+ (BOOL)date:(NSDate*)date isBetweenDate:(NSDate*)beginDate andDate:(NSDate*)endDate
{
    if ([date compare:beginDate] == NSOrderedAscending)
        return NO;

    if ([date compare:endDate] == NSOrderedDescending) 
        return NO;

    return YES;
}
```