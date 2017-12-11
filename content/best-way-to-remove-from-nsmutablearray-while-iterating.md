# NSMutableArray遍历移除的最好方式？
[Best way to remove from NSMutableArray while iterating?](https://stackoverflow.com/questions/111866/best-way-to-remove-from-nsmutablearray-while-iterating)

___



> 1

为了清晰，我一般是是先初始化一个数组用来收集要删除的项目，然后再从原来的数组里删除它：

```objc
NSMutableArray *discardedItems = [NSMutableArray array];
SomeObjectClass *item;

for (item in originalArrayOfItems) {
    if ([item shouldBeDiscarded])
        [discardedItems addObject:item];
}

[originalArrayOfItems removeObjectsInArray:discardedItems];
```

> 2

其他的答案会有低效问题当一个大的数组要遍历。因为方法 `removeObject:` 和 `removeObjectsInArray:` 要做一个线性搜索, 这是一个浪费因为其实你已经知道对象在哪里了.同样，任何调用 `removeObjectAtIndex:` 在短时内要copy从索引到最后的值。

更高效的方式应该是这样：

```Objc
NSMutableArray *array = ...
NSMutableArray *itemsToKeep = [NSMutableArray arrayWithCapacity:[array count]];
for (id object in array) {
    if (! shouldRemove(object)) {
        [itemsToKeep addObject:object];
    }
}
[array setArray:itemsToKeep];
```

