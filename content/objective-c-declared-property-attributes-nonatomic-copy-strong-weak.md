# Objective-C属性修饰符(nonatomic, copy, strong, weak)？
[Objective-C declared @property attributes (nonatomic, copy, strong, weak)](https://stackoverflow.com/questions/9859719/objective-c-declared-property-attributes-nonatomic-copy-strong-weak)

___



> 1

**Nonatomic**

`nonatomic` 被用于多线程编程.如果我们在声明时用nonatomic修饰属性, 那么在多线程的时候，其他线程也可以同时访问该属性.

**Copy**

`copy` 在可变对象的时候需要. 你不希望你的对象的改变会被其他可变对象所影响，在用完之后会被释放.

**Assign**

`Assign` 与 `copy`.相反，当你访问 `assign` 属性, 会直接返回一个真实值. 一般你在使用基础值类型 (float, int, BOOL...)

**Retain**

`retain` 被用在当一个指针指向一个对象. setter方法被 `@synthesize` 将 retain (引用计数加一) 这个对象. 当你用完这个对象你需要释放它. 用retain将会使对象的引用计数加一

**Strong**

`strong` 是 Automated Reference Counting (ARC).用来替换retain的.

**Weak**

`weak` 与 `strong` 类似，用于指针对象，但是不会使引用计数加1.它不会成为对象的所有者，只是与对象保持一份引用关系.如果对象的引用计数归为0，即使有weak指针指向它，依旧会被dealloc。

当weak指针指向的对象被dealloc时，weak指针会被置为nil.