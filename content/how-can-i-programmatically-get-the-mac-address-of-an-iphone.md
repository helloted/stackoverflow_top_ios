# 设备唯一标识
[How can I programmatically get the MAC address of an iphone](https://stackoverflow.com/questions/677530/how-can-i-programmatically-get-the-mac-address-of-an-iphone)

___



> 1

在iOS7之后，不能获取设备的Mac地址，会返回02:00:00:00:00:00

设备的唯一标识

import "UIDevice+Identifier.h"

```objc
- (NSString *) identifierForVendor1
{
    if ([[UIDevice currentDevice] respondsToSelector:@selector(identifierForVendor)]) {
        return [[[UIDevice currentDevice] identifierForVendor] UUIDString];
    }
    return @"";
}
```

