# UIView的frame, bounds, center？
[UIView frame, bounds and center](https://stackoverflow.com/questions/5361369/uiview-frame-bounds-and-center)

___



> 1

**Frame** : `frame` (`CGRect`)是一个相对于 `superview`坐标系统的一个长方形. 默认开始是从左上.

**Bounds**: `bounds` (`CGRect`) 表示的是一个以自己坐标系统为基准的长方形

**Center** : `center`  `CGPoint` 是在 `superview`的坐标系统上，View的中心位置

他们之间的关系如下：

- `frame.origin = center - (bounds.size / 2.0)`
- `center = frame.origin + (bounds.size / 2.0)`
- `frame.size = bounds.size`

![img](/images/04.jpg)

> 2

1、UIView中，frame其实是不存储的，而是动态计算的，改变center，改变bounds大小，或者改变transfrom都可能会导致frame的改变。 

![img](/images/16.jpg)

2、Bounds的orgin并不总是(0,0)，比如UIScrollView向上滑动，就有可能是(0,-10)

3、 transform不会影响到view的bounds和center，但是会影响到frame。 比如大小缩小到0.9倍，则center不变，frame.size 变为 0.9倍，origin也会跟着变。

frame.size = bounds.size
frame.origin.x = center.x - bounds.size.width / 2
frame.origin.y = center.y - bounds.size.height / 2