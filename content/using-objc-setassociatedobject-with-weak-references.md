# 如何objc_setAssociatedObject关联weak属性
[Using objc_setAssociatedObject with weak references](https://stackoverflow.com/questions/16569840/using-objc-setassociatedobject-with-weak-references)

 有OBJC_ASSOCIATION_ASSIGN这个选项，但是会不会在引用会回收后将指针置为nil?

___



> 1

`OBJC_ASSOCIATION_ASSIGN` 不会在属性清空后将引用指针清空，这会造成野指针，所以是由风险去访问一个已经被清除的对象的。但是我们可以用另外的一种方法来关联一个weak属性，那就是强关联一个对象，然后让这个对象来弱引用这个属性。

```objc
@interface WeakObjectContainer : NSObject
@property (nonatomic, readonly, weak) id object;
@end

@implementation WeakObjectContainer
- (instancetype) initWithObject:(id)object
{
    if (!(self = [super init]))
        return nil;

    _object = object;

    return self;
}
@end
```

把WeakObjectContainer对象用OBJC_ASSOCIATION_RETAIN_NONATOMIC强关联

```objc
objc_setAssociatedObject(self, &MyKey, [[WeakObjectContainer alloc] initWithObject:object], OBJC_ASSOCIATION_RETAIN_NONATOMIC);
```

```objc
id object = [objc_getAssociatedObject(self, &MyKey) object];
```