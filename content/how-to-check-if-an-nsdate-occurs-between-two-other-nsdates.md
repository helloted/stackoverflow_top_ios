# 判断一个时间在另外两个时间之间
[How to Check if an NSDate occurs between two other NSDates](https://stackoverflow.com/questions/1072848/how-to-check-if-an-nsdate-occurs-between-two-other-nsdates)

___



> 1

```objc
+ (BOOL)date:(NSDate*)date isBetweenDate:(NSDate*)beginDate andDate:(NSDate*)endDate
{
  	// 在开始之间之前
    if ([date compare:beginDate] == NSOrderedAscending)
        return NO;

  	// 在结束时间之后
    if ([date compare:endDate] == NSOrderedDescending) 
        return NO;

    return YES;
}
```

