# release
自定义的发布过程，我们认为发布包括构建、部署两部分并且遵循**“开发代码和发布代码分离”**的原则

- build: 构建相关的配置
- code: 发布代码
- deploy: 部署相关的配置

## build 
TODO

## deploy
We use [deliver](https://github.com/fastlane/fastlane/tree/master/deliver) to upload screenshots, metadata and your app to the App Store using a single command.
deliver is part of [fastlane](https://github.com/fastlane/fastlane) : The easiest way to automate building and releasing your iOS and Android apps.

### Installation deliver
```
sudo gem install fastlane --verbose
sudo gem install deliver
```
Make sure, you have the latest version of the Xcode command line tools installed:
```
xcode-select --install
```

_**PS**_:
deliver的安装在国内会被墙，可选择使用国内淘宝的镜像
```
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
```

### Config deliver
You can config deploying info in **Deliverfile**. 
Please notice to config your **username** and **app_identifier**. You can contact your leader to get it.

Then copy app's screenshots into **screenshots/\<localisation\>**. 
Screenshots size:

- 3.5-Inch (iPhone 3,4,4s)
    - 640 × 920px portrait (without status bar) minimum
    - 640 × 960px portrait (full screen) maximum
    - 960 × 600px landscape (without status bar) minimum
    - 960 × 640px landscape (full screen) maximum
- 4-Inch (iPhone 5,5s)
    - 640 × 1096px portrait (without status bar) minimum
    - 640 × 1136px portrait (full screen) maximum
    - 1136 × 600px landscape (without status bar) minimum
    - 1136 × 640px landscape (full screen) maximum
- 4.7-Inch (iPhone 6)
    - 750 × 1334px portrait
- 5.5-Inch (iPhone 6 Plus)
    - 1242 × 2208px portrait
- iPad (Air and Mini Retina)
    - 1536 x 2048
- iPad Pro
    - 2048 x 2732
- Apple Watch
	- 312 x 390

You can create it use [Screenshot Builder](https://launchkit.io)

### New App in iTunes Connect
Please send **Deliverfile** to your leader and ask for creating a new app in **iTunes Connect**

### Deploy to App Store
```
deliver
```
You will be prompted to enter your iTunes Connect credentials. You can contact your leader to get it which will be stored in the Mac OS X keychain.