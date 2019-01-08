# UINavigationController在pushViewController时卡顿？
___



> 1

进行开发中，遇到了个小问题：

在使用UINavigationController的-pushViewController:animated:执行入栈一个子控制器操作时(即最新栈顶子控制器)，会出现推出(即入栈)"卡顿"现象，

原因：这是因为从iOS7开始， UIViewController的根view的背景颜色默认为透明色(即clearColor)，所谓"卡顿"其实就是由于透明色重叠后，造成视觉上的错觉，所以这并不是真正的"卡顿"，但这种"卡顿"现象还是让人觉得极其不舒服的，还是务必得解决的！

解决方法：只要在该UINavigationController所push的那个子控制器C(C即当前最新栈顶子控制器)中赋值其根view的背景颜色为某种颜色，即取缔默认的透明色  (即clearColor)，就能解决所谓的"卡顿"问题啦！

 self.view.backgroundColor = [UIColor whiteColor];