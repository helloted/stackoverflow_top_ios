# NSURL里的部分信息
[Get parts of a NSURL in objective-c](https://stackoverflow.com/questions/3692947/get-parts-of-a-nsurl-in-objective-c)

___



> 1

```
http://foobar:nicate@example.com:8080/some/path/file.html;params-here?foo=bar#baz
```

对于上面这样的一个URL，通过实例方法可以获取部分信息

- `-[NSURL scheme]` = http
- `-[NSURL resourceSpecifier]` = (从 // 到 URL的结尾)
- `-[NSURL user]` = foobar
- `-[NSURL password]` = nicate
- `-[NSURL host]` = example.com
- `-[NSURL port]` = 8080
- `-[NSURL path]` = /some/path/file.html
- `-[NSURL pathComponents]` = @["/", "some", "path", "file.html"] (note that the initial / is part of it)
- `-[NSURL lastPathComponent]` = file.html
- `-[NSURL pathExtension]` = html
- `-[NSURL parameterString]` = params-here
- `-[NSURL query]` = foo=bar
- `-[NSURL fragment]` = baz