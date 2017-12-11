# nil, NIL, NULL, NSNull的区别？
[Difference between nil, NIL and, null in Objective-C](https://stackoverflow.com/questions/5908936/difference-between-nil-nil-and-null-in-objective-c)

___



> 1

#### nil

`nil` 是 Objective-C 对象空值的意思, 对应于未知类型  `id` 或者其他 Objective-C类型的对象 。

```objc
NSString *someString = nil;
NSURL *someURL = nil;
id someObject = nil;

if (anotherObject == nil) // do something
```

#### Nil

`Nil` 是 Objective-C 类为空, 对应于 `Class`. 因为大部分代码不需要引用class变量，所以这个并不常用。

```objc
Class someClass = Nil;
Class anotherClass = [NSString class];
```

#### NULL

`NULL` C指针为空值。

```objc
int *pointerToInt = NULL;
char *pointerToChar = NULL;
struct TreeNode *rootNode = NULL;
```

#### NSNull

`NSNull` 是一个类用来代表空对象，实际上就是 `+[NSNull null]`. 与 `nil` 不一样因为空 `nil` 就是字面上的孔不是一个对象.  `NSNull`的实例对象，是一个对象。

`NSNull` 经常用在 Foundation collections 因为它们不能存储 `nil` 值. 比如在dictionaries, `-objectForKey:` 返回一个 `nil` 对应的key没有存储对象在里面,这个key没有添加进字典里. 如果你想用来表明，这个kety清楚地被添加进了，只不过没有值，你应该用 `[NSNull null]`.

```objc
NSMutableDictionary *dict = [NSMutableDictionary dictionary];
[dict setObject:[NSNull null] forKey:@"someKey"];

// 下面这种赋值时错误的，因为不能设nil
NSMutableDictionary *dict = [NSMutableDictionary dictionary];
[dict setObject:nil forKey:@"someKey"];
```

对于nil,只有在NSArray初始化时在作为结束的一个标志。这种情况也不是作为元素存储。

```
NSArray *array = [NSArray arrayWithObjects:@"one", @"two", nil];
```