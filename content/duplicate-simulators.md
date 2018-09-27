# Xcode重复出现多个模拟器的处理方法？
___



> 1

首先完全退出Xcode和模拟器

然后在终端输入：

```shell
sudo killall -9 com.apple.CoreSimulator.CoreSimulatorService

rm -rf ~/Library/Developer/CoreSimulator/Devices
```