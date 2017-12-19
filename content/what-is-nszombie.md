# 什么是僵尸对象
[What is NSZombie?](https://stackoverflow.com/questions/4168327/what-is-nszombie)

___



> 1

这是一个内存检测助手. 特别地当你设置 `NSZombieEnabled` ，如果有一个对象的引用计数为 0, 相比于被回收，它会把自己变成 `NSZombie`实例对象，也就是僵尸对象. 当这个对象收到了方法消息, 它会在奔溃的位置显示出来，并且打印出日志为什么有问题。这样就可以检查到野指针。

野指针：指向已经被释放的对象。

错误：EXC_BAD_ACCESS/EXC_BAD_INSTRUCTION

> 2

这样一段代码

```objc
static NSMutableArray*array;
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    array= [[NSMutableArray alloc]initWithCapacity:5];
    [array release];//释放掉该数组
}

- (void)viewDidAppear:(BOOL)animated{
    [array addObject:@"Hello"];//使用释放掉的数组
}
```

开启僵尸对象之前：

![img](/images/10.png)

开启僵尸对象：

![img](/images/11.png)

开启僵尸对象之后：

![img](/images/12.png)



