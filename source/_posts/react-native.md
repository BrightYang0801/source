---
title: macOS系统下的React Native 开发环境配置
date: 2018-08-31 21:38:40
tags: 
- react-native
categories: 
- react-native
---

1. ** Homebrew安装 **
Homebrew是一款自由及开放源代码的软件包管理系统，用以简化Mac OS X系统上的软件安装过程，Homebrew以Ruby语言写成，针对于Mac OS X操作系统自带Ruby的版本。默认安装在/usr/local，由一个核心git版本库构成，以使用户能更新Homebrew。是 OS X 不可或缺的套件管理器。
安装之前，你可以先检查一下电脑上是否已经安装了Homebrew，检查方式如下：
在终端执行下列命令：
```
 brew -v
```
    如果已经安装了，终端会显示版本号。
    如果没有安装，那就可以用下面这种方式，进行安装，在终端上直接输入下面的命令即可：
```
  ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```
2. ** node.js安装 **
```
nvm install node && nvm alias default node

```
3. ** 安装watchman 和 flow **
```
brew install watchman
brew install flow

```
4. ** 安装React Native **
我们使用npm进行安装，如下：
```
npm install -g react-native-cli

```
    安装完React Native之后，要想运行或者初始化一个项目，然后运行到模拟器或者真机，我们需要搭建一个Android或者ios开发环境，我这里只介绍android，相信想学习React Native的同学，电脑上都基本上有了Android的开发环境。但是可能会有坑，有一个大坑就是得配置SDK的环境变量：ANDROID_HOME。
5. ** SDK环境变量的配置 **
- 启动Terminal终端工具
- 输入cd ~/ 进入当前用户的home目录
- 创建
```
touch .bash_profile
```
    打开并编辑：
```
open .bash_profile
```
    在文件中写入以下内容：
```
export PATH=${PATH}:/Users/loonggg/Application/android-sdk-mac_x86/tools:/Users/loonggg/Application/android-sdk-mac_x86/platform-tools

```
    友情提示：上述路径，请换成自己电脑上的SDK所在路径

- 执行如下命令：
```
source .bash_profile
```
- 验证：输入adb回车。如果未显示command not found，说明此命令有效，环境便设置完成。
6. ** 创建我们的第一个React Native应用 **
 + 初始化项目
  上面的AwesomeProject这个项目名字，你可以自己随意定义，自己命名，没有限制。
 + 运行项目
   切换到AwesomeProject的主目录
   运行项目命令
   ```
   react-native run-android
   react-native run-ios
   ```
    执行react-native run-ios 遇到下面错误：
    xcrun: error: unable to find utility "instruments", not a developer tool or in PATH
    ```
    sudo xcode-select -s /Applications/Xcode.app/Contents/Developer/

    ```
    我们使用编辑器打开和修改app.js文件，调出模拟器菜单键，选择重新载入 js 即可看到变化。
    执行react-native run-android 遇到下面错误
    java.lang.RuntimeException: SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable.
    解决方法：在工程的根目录下的android文件下新建一个local.properties的文件，在文件中写入
    sdk.dir = /Users/jinwenfeng/Documents/android/android-sdk-macosx
    这里就是androidsdk的路径，至此问题一成功解决
 + 安卓打包
   ```
   cd android && ./gradlew assembleRelease

   ```


