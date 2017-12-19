# APNs的Token创建后会更新吗？
[Does the APNS device token ever change, once created?](https://stackoverflow.com/questions/6652242/does-the-apns-device-token-ever-change-once-created)

___



> 1

[APNS](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1)

> Never cache device tokens in your app; instead, get them from the system when you need them. APNs issues a new device token to your app when certain events happen. The device token is guaranteed to be different, for example, when a user restores a device from a backup, when the user installs your app on a new device, and when the user reinstalls the operating system. Fetching the token, rather than relying on a cache, ensures that you have the current device token needed for your provider to communicate with APNs. When you attempt to fetch a device token but it has not changed, the fetch method returns quickly.

不要缓存device tokens，相反，你应该在需要的时候去获取它， APNs 会在一些特定情况下更新token，比如，当用户从备份里恢复一个设备，用户安装APP到一个新设备，用户重新安装系统。所以不要去依赖缓存token，而应当在需要的时候去获取。