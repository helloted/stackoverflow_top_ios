# 数组存储结构体
[What's the best way to put a c-struct in an NSArray?](https://stackoverflow.com/questions/4516991/whats-the-best-way-to-put-a-c-struct-in-an-nsarray)

___



> 1

通过[NSValue](https://developer.apple.com/documentation/foundation/nsvalue)的变体Categroy来实现

> An `NSValue` object can hold any of the scalar types such as `int`, `float`, and `char`, as well as pointers, structures, and object `id` references. Use this class to work with such data types in collections (such as [`NSArray`](https://developer.apple.com/documentation/foundation/nsarray) and [`NSSet`](https://developer.apple.com/documentation/foundation/nsset)), [Key-value coding](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/KeyValueCoding.html#//apple_ref/doc/uid/TP40008195-CH25), and other APIs that require Objective-C objects. `NSValue` objects are always immutable.

一个NSValue可以存储任何的数值类型比如Int,float,char，同样也适用于指针，结构体，id对象.这个类可以用于结合类、KVC或者其他API需要OC对象的时候。

```objc
typedef struct {
    int numFaces;
    float radius;
} Polyhedron;
 
@interface NSValue (Polyhedron)
+ (instancetype)valuewithPolyhedron:(Polyhedron)value;
@property (readonly) Polyhedron polyhedronValue;
@end
 
@implementation NSValue (Polyhedron)
+ (instancetype)valuewithPolyhedron:(Polyhedron)value
{
    return [self valueWithBytes:&value objCType:@encode(Polyhedron)];
}
- (Polyhedron) polyhedronValue
{
    Polyhedron value;
    [self getValue:&value];
    return value;
}
@end
```

数组里存储NSValue就行了