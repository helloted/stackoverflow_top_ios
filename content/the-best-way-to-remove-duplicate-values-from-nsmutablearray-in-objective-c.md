# 数组去重
[The best way to remove duplicate values from NSMutableArray in Objective-C?](https://stackoverflow.com/questions/1025674/the-best-way-to-remove-duplicate-values-from-nsmutablearray-in-objective-c)

___



> 1

如果不用考虑顺序的话，用NSSet

```
NSOrderedSet *orderedSet = [NSOrderedSet orderedSetWithArray:yourArray];
NSArray *arrayWithoutDuplicates = [orderedSet array];
```

> 2

用 [Object Operators from Key Value Coding](http://nshipster.com/kvc-collection-operators/) 

```
uniquearray = [yourarray valueForKeyPath:@"@distinctUnionOfObjects.self"];
```