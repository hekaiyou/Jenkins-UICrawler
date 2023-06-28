# Jenkins-UICrawler

结合Jenkins、UICrawler实现自动化UI遍历。

## Windows 环境搭建

### JAVA

检查 java 命令, 没有的话需要安装。

```shell
java -version
```

配置 JAVA_HOME 环境变量（可以用 `java -verbose` 命令查看安装路径）。

```shell
JAVA_HOME = X:\xxx\xxx\Java\jre1.x.x_xxx
```

### Android SDK

下载 Android SDK 压缩包, 例如这里下载 android-sdk_r24.4.1-windows.zip 并解压到任意目录下, 重命名为 android-sdk, 然后打开 android-sdk 下的 Manager.exe 文件, 安装下面的内容。

- Tools
   - Android SDK Platform-tools
   - Android SDK Build-tools
- Extras
   - Google USB Driver

配置 ANDROID_HOME 环境变量。

```shell
ANDROID_HOME = X:\xxx\xxx\android-sdk
```

在 Path 环境变量里添加一行配置。

```shell
%ANDROID_HOME%\platform-tools
```

检查 adb 命令。

```shell
adb version
```

### Appium Server GUI

下载 Appium-Server-GUI 安装包, 例如这里下载 Appium-Server-GUI-windows-1.22.3-4.exe 文件并安装, 然后启动它, 点击 Start Server 直接启动服务。

### UICrawler

下载 Jenkins-UICrawler 项目代码。

```shell
git clone https://github.com/hekaiyou/Jenkins-UICrawler.git
```

进入项目目录下, 打开 config.yml 文件, 以 Calculator(计算器) 应用为例,替换两个参数

- ANDROID_PACKAGE: App包名
   ```shell
   adb shell
   pm list package
   pm list package | grep calculator
   exit
   ```
- ANDROID_MAIN_ACTIVITY: App启动的Activity
   ```shell
   adb shell
   dumpsys package com.google.android.calculator
   exit
   ```

### RUN

检查 Android 是否连接正常, 且确认 Android 开发者选项相关开启, 复制手机 ID 字符串

```shell
adb devices -l
```

执行自动化元素遍历测试

```shell
java -jar UICrawler-2.3.7.jar -f config.yml -u 手机ID
```
