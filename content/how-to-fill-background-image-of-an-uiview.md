# 背景图片充满UIViw？
[How to fill background image of an UIView](https://stackoverflow.com/questions/8077740/how-to-fill-background-image-of-an-uiview)

我有一个UIView，然后设置了一个背景图片

```c
self.view.backgroundColor = [UIColor colorWithPatternImage:[UIImage imageNamed:@"sfond-appz.png"]];
```

问题在于，背景图片并不是在View中居中，而是重复了几次来填满整个View，是否有方法来填充这个View？

___



> 1

你需要先处理一下图片，像下面这样：

```c
UIGraphicsBeginImageContext(self.view.frame.size);
[[UIImage imageNamed:@"image.png"] drawInRect:self.view.bounds];
UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
UIGraphicsEndImageContext();

self.view.backgroundColor = [UIColor colorWithPatternImage:image];
```