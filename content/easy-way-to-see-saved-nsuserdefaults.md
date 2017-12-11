# 查看存储在NSUserDefaults的值
[Easy way to see saved NSUserDefaults?](https://stackoverflow.com/questions/1676938/easy-way-to-see-saved-nsuserdefaults)

___



> 1

在模拟器中的APP，你可以去这个路径查看

```
/users/your user name/Library/Application Support/iPhone Simulator/<Sim Version>/Applications
```

这个目录有一个GUID文件夹，如果你有好几个APP在里面，会有几个文件夹，所以你应该找到你的app binary:

```
find . -name foo.app
./1BAB4C83-8E7E-4671-AC36-6043F8A9BFA7/foo.app
```

然后去对应的文件夹：

```
cd 1BAB4C83-8E7E-4671-AC35-6043F8A9BFA7/Library/Preferences
```

你应该可以看到一个文件：

```
<Bundle Identifier>.foo.pList
```

打开这个文件夹就能找到你要的值了

> 2

可以再log里打印出来：

Keys:

```
NSLog(@"%@", [[[NSUserDefaults standardUserDefaults] dictionaryRepresentation] allKeys]);
```

Keys and values:

```
NSLog(@"%@", [[NSUserDefaults standardUserDefaults] dictionaryRepresentation]);
```

