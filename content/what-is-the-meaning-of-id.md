# id类型是什么意思？
[What is the meaning of id?](https://stackoverflow.com/questions/7987060/what-is-the-meaning-of-id)

___



> 1

id是一个指针指向任何类型，但是与void *不同的是，id指向的是Objective-C对象，比如，你可以添加id类型的任何东西到NSArray，但是这些对象必需能够rerain和release.

编译器能够将任何对象隐式转换为id，并且可以将id转换为任何对象。 这与Objective-C中的任何其他隐式转换不同，并且是cocoa中大多数容器类型的基础。