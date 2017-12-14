# 取消performSelector:afterDelay
[cancelling queued performSelector:afterDelay calls](https://stackoverflow.com/questions/1806445/cancelling-queued-performselectorafterdelay-calls)

___



> 1

```
[NSObject cancelPreviousPerformRequestsWithTarget:]
```

或者

```
[NSObject cancelPreviousPerformRequestsWithTarget:selector:object:]
```

 `target` 是之前调用 `performSelector:afterDelay:` 的对象.

例如：

```objc
// schedule the selector
[self performSelector:@selector(mySel:) withObject:nil afterDelay:5.0];
// cancel the above call (and any others on self)
[NSObject cancelPreviousPerformRequestsWithTarget:self];
```

