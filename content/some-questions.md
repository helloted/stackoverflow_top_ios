# 总结几个知识点
___



> 一、第三方统计上传的策略

**友盟**

1. 启动时发送：默认
2. 按间隔发送：按特定间隔发送数据，间隔时长介于90秒与1天之间。

**腾讯**：

1. 实时发送;

2. 启动时发送;
3. 数量发送：默认当消息数量达到30条时发送一次。
4. Wifi发送：只在wifi状态下发送，非wifi情况缓存到本地。
5. 间隔发送：间隔一段时间发送，每隔一段时间一次性发送到服务器。

> 二、弱网优化

- 减小数据包大小和优化包量：压缩、精简包头、消息合并等方式，来减小数据包大小和包量。
- DNS查询优化：根据客户端IP和服务器接入点IP，返回最优的接入点列表，包括IP的排序，以及客户端接入的国家、省份、运营商、APN和网关。
- 控制数据包大小不超过1500，避免分片
- 优化TCP socket参数，包括：是否关闭快速回收、初始RTO、初始拥塞窗口、socket缓存大小、Delay-ACK、Selective-ACK、TCP_CORK、拥塞算法。
- 复用连接

> 三、启动优化

1、为什么合并第三方库可以加载更快？

dylib loading载入动态库阶段，这个过程中，会去装载app使用的动态库，而每一个动态库有它自己的依赖关系，所以会消耗时间去查找和读取。对于Apple提供的的系统动态库，做了高度的优化。而对于开发者定义导入的动态库，则需要在花费更多的时间。Apple官方建议尽量少的使用自定义的动态库，或者考虑合并动态库。

2、延迟初始化的策略？

答：建一个类来管理初始化，所有需要初始化的代码都在这里进行，分类初始化：

1)、日志 / 统计等需要第一时间启动的, 仍然伴随 didFinishLaunchingWithOptions 启动.

2)、用户数据需要在广告显示完成以后使用, 所以需要伴随广告页启动。

3)、比如分享业务, 肯定是用户能看到真正的主界面以后才需要启动, 所以推迟到主界面加载完成以后启动, 只需要将代码放到方法里。

> 四、ARC MRC下Block的区别

Block有三种Block:NSConcreteGlobalBlock, NSConcreteStackBlock，NSConcreteMallocBlock

- MRC情况：需要手动copy到堆中，也就是NSConcreteStackBlock> NSConcreteMallocBlock
- ARC情况：copy修饰NSConcreteStackBlock，会自动NSConcreteStackBlock> NSConcreteMallocBlock，也就是说，ARC下Block实际使用时只有NSConcreteGlobalBlock，NSConcreteMallocBlock两种

