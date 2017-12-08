# NSString的属性修饰符应该用copy还是strong(retain)？
[NSString property: copy or retain?](https://stackoverflow.com/questions/387959/nsstring-property-copy-or-retain)

___



> 1

#### 对于NSString，用copy修饰是不是比用retain修饰好？

是的，一般情况总是用copy修饰符

这是因为**NSString property**可能被**NSString**实例或者**NSMutableString**实例赋值, 所以我们没有办法确认传过来的对象是可变的还是不可变的

#### copy修饰属性是否比用retain修饰更低效？

- 如果你的属性被赋值传过来的是 **NSString实例**, 答案是 "**No**" - copy没有更低效(没有更低效的原因是不可变对象的copy依旧是浅拷贝).
- 如果你的属性被赋值而传过来的对象是 **NSMutableString实例对象**，那么答案就是 "**Yes**" - copying比retain更低效.(因为可变对象的复制时深拷贝)

#### 什么情况下使用copy?

你应该使用copy，当你不想属性的内部状态在毫无提示的情况下被更改(当传递的是可变对象，如果可变对象做了更改，那么这个属性也会跟着修改)。

#### 深拷贝，浅拷贝

- [immutableObject copy] // 浅复制
- [immutableObject mutableCopy] //深复制
- [mutableObject copy] //深复制
- [mutableObject mutableCopy] //深复制

