# 如何在NSMutableArray里对自定义对象进行排序？

https://stackoverflow.com/questions/805547/how-do-i-sort-an-nsmutablearray-with-custom-objects-in-it

问题：

drinkDetails是一个数组，有一个Person对象，里面有个类型为NSDate的birthDate属性，想根据这个属性对Person排序

___



> 1

#### Compare Method

在Person类里实现一个compare方法：

```
- (NSComparisonResult)compare:(Person *)otherObject {
    return [self.birthDate compare:otherObject.birthDate];
}

NSArray *sortedArray = [drinkDetails sortedArrayUsingSelector:@selector(compare:)];
```

#### NSSortDescriptor

```
NSSortDescriptor *sortDescriptor;
sortDescriptor = [[NSSortDescriptor alloc] initWithKey:@"birthDate"
                                           ascending:YES];
NSArray *sortedArray = [drinkDetails sortedArrayUsingDescriptors:@[sortDescriptor]];
```

#### Blocks

```
NSArray *sortedArray;
sortedArray = [drinkDetails sortedArrayUsingComparator:^NSComparisonResult(id a, id b) {
    NSDate *first = [(Person*)a birthDate];
    NSDate *second = [(Person*)b birthDate];
    return [first compare:second];
}];
```

效率

 `-compare:` 和block方法会更快一些, 一般来说，使用 `NSSortDescriptor` 依赖于KVC. 优势在于提供了一种方式通过使用data来进行排序而不是代码，这样的话，使得一些排序更容易，比如，用户可以通过点击header行来对 `NSTableView` 进行排序.