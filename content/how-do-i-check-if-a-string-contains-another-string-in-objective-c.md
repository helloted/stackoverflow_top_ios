# 如何判断一个字符串包含另外一个字符串？
https://stackoverflow.com/questions/2753956/how-do-i-check-if-a-string-contains-another-string-in-objective-c

___



> 1

```
NSString *string = @"hello bla bla";
if ([string rangeOfString:@"bla"].location == NSNotFound) {
  NSLog(@"string does not contain bla");
} else {
  NSLog(@"string contains bla!");
}
```

如果是iOS8以上可以用以下的方法，注意，如果是iOS7会导致崩溃

```
NSString *string = @"hello bla blah";
if ([string containsString:@"bla"]) {
  NSLog(@"string contains bla!");
} else {
  NSLog(@"string does not contain bla");
}
```

___

> 2

手动写一个算法:

核心思想：将a中的每个字符对应的素数相乘，得到一个整数。然后，让字符串b中的每一个字符也对应相应的素数，再用b中的每个字符对应的素数除上面得到的整数。如果有余数，说明结果为false，立即退出程序；如果整个过程中没有余数，则说明b是a的子集。

```
bool StringContain（string &a, string &b）
{
    const int p[26]={2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,
                     59,61,67,71,73,79,83,89,97,101};
    int result=1;//存放字符串a每个字符对应素数的乘积
    for(int i=0; i<a.length(); i++)
    {
        int x = p[a[i] - 'A'];
        if(result % x)
        {
            result *= x;
        }
    }
    for(int i=0; i<b.length(); i++)
    {
        int x=p[b[i] - 'A'];
        if(resuilt % x)
            return false;
    }
    return true;
}
```

