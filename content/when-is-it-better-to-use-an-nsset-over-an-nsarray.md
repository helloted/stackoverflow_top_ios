# NSSet vs. NSArray
[When is it better to use an NSSet over an NSArray?](https://stackoverflow.com/questions/10997404/when-is-it-better-to-use-an-nsset-over-an-nsarray)

___



> 1

[苹果官方文档](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Collections/Collections.html)

![img](/images/07.png)

最大的不同就是NSArray是一个有序的集合，NSSet是一个无序的集合。查找某个对象NSSet会比较快，因为NSSet是通过hashkey来查找，而NSArray是通过遍历整体才能查找到。

如果你想遍历一个结合，不需要有序，NSSet性能更好，插入和删除都更快，但是很多情况，有些事情只有NSArray可以做。

**NSSet**

- 主要通过比较来获取项目
- 无序
- 不允许重复
- 快速插入、删除和查看是否存在某个item

**NSArray**

- 可以根据序号来获取项目
- 有序
- 允许重复