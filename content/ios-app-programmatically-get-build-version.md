# 获取APP的版本信息
[iOS app, programmatically get build version](https://stackoverflow.com/questions/16888780/ios-app-programmatically-get-build-version)

___



> 1

 "Version"号 :

Swift 3

```swift
let version = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as! String
```

ObjC

```Objc
NSString *version = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"];
```

"Build"号:

Swift 3

```swift
let build = Bundle.main.infoDictionary?[kCFBundleVersionKey as String] as? String
```

ObjC

```ojbc
NSString *build = [[[NSBundle mainBundle] infoDictionary] objectForKey:(NSString *)kCFBundleVersionKey];
```

