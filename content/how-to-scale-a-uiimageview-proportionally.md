# UIImageView的伸缩模式
[How to scale a UIImageView proportionally?](https://stackoverflow.com/questions/185652/how-to-scale-a-uiimageview-proportionally)

___



> 1

![img](/images/03.png)

#### ScaletoFill:

四面拉伸图片直到四边都填满整个ImageView，这个有可能会导致图片变形

#### Aspect Fit:

拉伸图片直到最大边与View的边相匹配，有可能导致另外一个方向的空余

#### Aspect Fill:

伸缩图片直到最小边与View的边相匹配，有可能导致另外一个方向的超出区域