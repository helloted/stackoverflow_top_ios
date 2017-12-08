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

![img](/images/04.png)