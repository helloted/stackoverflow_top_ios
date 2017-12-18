# 数组过滤
[filtering NSArray into a new NSArray in objective-c](https://stackoverflow.com/questions/110332/filtering-nsarray-into-a-new-nsarray-in-objective-c)

___



> 1

`NSArray` 提供了 **filteredArrayUsingPredicate:** 方法来进行过滤

```objc
NSMutableArray *array = [NSMutableArray arrayWithObjects:@"Bill", @"Ben", @"Chris", @"Melissa", nil];

NSPredicate *bPredicate = [NSPredicate predicateWithFormat:@"SELF beginswith[c] 'b'"];
NSArray *beginWithB =  [array filteredArrayUsingPredicate:bPredicate];
// beginWithB contains { @"Bill", @"Ben" }.
```

或者用Block:

```objc
NSArray *filteredArray = [array filteredArrayUsingPredicate:[NSPredicate predicateWithBlock:^BOOL(id object, NSDictionary *bindings) {
    return [object shouldIKeepYou];  // Return YES for each object you want in filteredArray.
}]];
```

#### Swift:

```swift
nsArray = nsArray.filter { $0.shouldIKeepYou() }
```