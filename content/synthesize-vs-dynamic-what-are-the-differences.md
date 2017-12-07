# @synthesize vs @dynamic？
[@synthesize vs @dynamic, what are the differences?](https://stackoverflow.com/questions/1160498/synthesize-vs-dynamic-what-are-the-differences)

___



> 1

@synthesize 会自动给property属性自动生成getter方法和setter方法 . 

@dynamic 只是告诉编译器getter和setter方法不是由Class本身来声明，而是在其他地方生成(父类或者在runtime的时候生成)

如果在 `NSManagedObject` (CoreData)你想要创建一个属性的话。需要使用@dynamic。