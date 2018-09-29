# 字典数组的排序？
[Best way to sort an NSArray of NSDictionary objects?](https://stackoverflow.com/questions/2393386/best-way-to-sort-an-nsarray-of-nsdictionary-objects)

对一个字典数组的排序

___



> 1

使用NSSortDescriptor

```
NSSortDescriptor * descriptor = [[NSSortDescriptor alloc] initWithKey:@"interest" ascending:YES];
stories = [stories sortedArrayUsingDescriptors:@[descriptor]];
```

interest是字典里的key，stories是则是数组

