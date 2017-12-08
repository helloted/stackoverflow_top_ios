# objectForKey和valueForKey有什么区别？
[Difference between objectForKey and valueForKey?](https://stackoverflow.com/questions/1062183/difference-between-objectforkey-and-valueforkey)

___



> 1

`objectForKey:` 是一个 `NSDictionary` 方法. 一个 `NSDictionary` 是一个集合类如同 `NSArray`, 除了不能用index来取值, 用key来区分不同的item.key就是你提供的字符串. 没有两个对象有相同的key的可能 (就如同 `NSArray`里的对象不会有相同的序号 ).

`valueForKey:` 是一个KVC方法. 任何class都适用这个方法. `valueForKey:` 可以让你通过它的key来获取这个对象.

例如， 对于实例对象，我有一个 `Account` 类有个属性 `accountNumber`, 我可以这样:

```objc
NSNumber *anAccountNumber = [NSNumber numberWithInt:12345];
Account *newAccount = [[Account alloc] init];

[newAccount setAccountNumber:anAccountNUmber];

NSNumber *anotherAccountNumber = [newAccount accountNumber];
```

通过KVC，我可以动态的获取这个对象

```objc
NSNumber *anAccountNumber = [NSNumber numberWithInt:12345];
Account *newAccount = [[Account alloc] init];
[newAccount setValue:anAccountNumber forKey:@"accountNumber"];
NSNumber *anotherAccountNumber = [newAccount valueForKey:@"accountNumber"];
```

