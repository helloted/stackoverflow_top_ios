# NSMutableArray遍历移除的最好方式？
[Best way to remove from NSMutableArray while iterating?](https://stackoverflow.com/questions/111866/best-way-to-remove-from-nsmutablearray-while-iterating)

[NSEnumerator](https://developer.apple.com/documentation/foundation/nsenumerator)

> You send [`nextObject()`](https://developer.apple.com/documentation/foundation/nsenumerator/1409616-nextobject) repeatedly to a newly created `NSEnumerator` object to have it return the next object in the original collection. When the collection is exhausted, `nil` is returned. You cannot “reset” an enumerator after it has exhausted its collection. To enumerate a collection again, you need a new enumerator.

快速遍历的原理是根据enumerator对象内部的计数器,调用nextObject方法来实现返回下一个数组元素的,直到元素全部返回就会返回nil,于是整个enumerator对象就遍历完了;同时也提醒,以这种原理来遍历enumerator对象的话,无论对这个对象做什么操作,对象的计数器都不会被重置!

可能是我们在快速遍历的时候,移除掉一个元素,但是计数器依旧是原来的,那么在遍历到最后会继续调用nextObject方法,而此时实际上已经全部遍历完了,但是系统并不知道,还在遍历,也就是越界;当发现没有元素时,就crash了

> In Objective-C, it is not safe to modify a mutable collection while enumerating through it. Some enumerators may currently allow enumeration of a collection that is modified, but this behavior is not guaranteed to be supported in the future.

遍历的时候不能对数组元素做删除操作

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

