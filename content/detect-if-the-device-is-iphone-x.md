# 判断设备型号iphone X
[Detect if the device is iPhone X](https://stackoverflow.com/questions/46192280/detect-if-the-device-is-iphone-x)

___



> 1

可以根据设备屏幕的大小来判断设备型号

![img](/images/09.png)

**swift 3 and above**

```swift
if UIDevice().userInterfaceIdiom == .phone {
        switch UIScreen.main.nativeBounds.height {
        case 1136:
            print("iPhone 5 or 5S or 5C")
        case 1334:
            print("iPhone 6/6S/7/8")
        case 2208:
            print("iPhone 6+/6S+/7+/8+")
        case 2436:
            print("iPhone X")
        default:
            print("unknown")
        }
    }
```

**objective C**

```objc
    if([[UIDevice currentDevice]userInterfaceIdiom]==UIUserInterfaceIdiomPhone) {

        switch ((int)[[UIScreen mainScreen] nativeBounds].size.height) {

            case 1136:
                printf("iPhone 5 or 5S or 5C");
                break;
            case 1334:
                printf("iPhone 6/6S/7/8");
                break;
            case 2208:
                printf("iPhone 6+/6S+/7+/8+");
                break;
            case 2436:
                printf("iPhone X");
                break;
            default:
                printf("unknown");
        }
    }
```