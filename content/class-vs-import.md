# @class vs. #import？
[@class vs. #import](https://stackoverflow.com/questions/322597/class-vs-import)

___



> 1

如果你`@class MyCoolClass`,编译器会这样

```
MyCoolClass *myObject;
```

编译器除了需要`MyCoolClass` 是一个可用的类，不需要关心其他的，它应该保留一个空间来存放一个指针来指向。这样，在头文件里，`@class`可以节省90%的时间。

然而，如果你需要创建或者接近myobject的成员，你需要让编译器知道这些方法是什么，这种情况下，你需要`#import "MyCoolClass.h"`, 用来告诉编译器附加信息而不只是说‘这是一个类’