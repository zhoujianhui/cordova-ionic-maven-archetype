#cordova-icon-splash
Automatically generate icons and splash screens from source images to create each size needed for each platform.
Since each platform has different image requirements, it’s best to make a source image for the **largest size needed**, and let the cordova-icon-splash do all the resizing, cropping and copying for you. 

本工具没有实现将icon和splash放到对应平台的资源目录下或者添加配置到cordova项目的config.xml，因为我们还需要此工具为原生项目开发服务。

对于Cordova项目可自行配置<pltforms>中有关icon和splash的配置。During the build process, Cordova (v3.6 or later) will look through the project’s config.xml file and copy the newly created resource images to the platform’s specific resource folder. 

##Usage
1、新建文件夹，如icon-splash，用于存放配置文件、原始图片资源和生成的图片资源。

2、新建配置文件，cordova-icon-splash默认配置文件为**icon-splash-config.json**。配置生成如下平台的资源：
```JSON
{
  "platforms": [
    "android",
    "ios"
  ]
}
```
*PS*: 生成Icon和Splash还有其它的配置项，默认内置在cordova-icon-splash，可通过icon-splash-config.json修改这些配置。

3、在在icon-splash中添加原始的icon.png和splash.png。建议大小为：

- icon: 1024 x 1024 (or even 2048 x 2048)
- splash: 2208x2208 with main content in center 1200x1200

4、安装cordova-icon-splash：
事先需要安装[ImageMagick](http://www.imagemagick.org),本工具使用其处理图片。
如果你使用OS X：
```
brew install imagemagick
```

安装完成之后，全局安装cordova-icon-splash
```
npm install cordova-icon-splash -g
```

生成：
```
cd icon-splash
cordova-icon-splash
```

## Config Icon and Splash For Cordova
在Cordova项目的config.xml中添加如下配置：
```XML
<platform name="android">
        ...

        <!-- Config Android Icon -->
        <icon src="icon-splash/android/icons/icon-ldpi.png" density="ldpi"/>
        <icon src="icon-splash/android/icons/icon-mdpi.png" density="mdpi"/>
        <icon src="icon-splash/android/icons/icon-hdpi.png" density="hdpi"/>
        <icon src="icon-splash/android/icons/icon-xhdpi.png" density="xhdpi"/>

        <!-- Config Android Splash -->
        <splash src="icon-splash/android/splashes/splash-land-hdpi.png" density="land-hdpi"/>
        <splash src="icon-splash/android/splashes/splash-land-ldpi.png" density="land-ldpi"/>
        <splash src="icon-splash/android/splashes/splash-land-mdpi.png" density="land-mdpi"/>
        <splash src="icon-splash/android/splashes/splash-land-xhdpi.png" density="land-xhdpi"/>
        <splash src="icon-splash/android/splashes/splash-port-hdpi.png" density="port-hdpi"/>
        <splash src="icon-splash/android/splashes/splash-port-ldpi.png" density="port-ldpi"/>
        <splash src="icon-splash/android/splashes/splash-port-mdpi.png" density="port-mdpi"/>
        <splash src="icon-splash/android/splashes/splash-port-xhdpi.png" density="port-xhdpi"/>
    </platform>
    <platform name="ios">
        ...

        <!-- Config iOS Icon -->
        <!-- iOS 8.0+ -->
        <!-- iPhone 6 Plus  -->
        <icon src="icon-splash/ios/icons/icon-60@3x.png" width="180" height="180"/>
        <!-- iOS 7.0+ -->
        <!-- iPhone / iPod Touch  -->
        <icon src="icon-splash/ios/icons/icon-60.png" width="60" height="60"/>
        <icon src="icon-splash/ios/icons/icon-60@2x.png" width="120" height="120"/>
        <!-- iPad -->
        <icon src="icon-splash/ios/icons/icon-76.png" width="76" height="76"/>
        <icon src="icon-splash/ios/icons/icon-76@2x.png" width="152" height="152"/>
        <!-- iOS 6.1 -->
        <!-- Spotlight Icon -->
        <icon src="icon-splash/ios/icons/icon-40.png" width="40" height="40"/>
        <icon src="icon-splash/ios/icons/icon-40@2x.png" width="80" height="80"/>
        <!-- iPhone / iPod Touch -->
        <icon src="icon-splash/ios/icons/icon.png" width="57" height="57"/>
        <icon src="icon-splash/ios/icons/icon@2x.png" width="114" height="114"/>
        <!-- iPad -->
        <icon src="icon-splash/ios/icons/icon-72.png" width="72" height="72"/>
        <icon src="icon-splash/ios/icons/icon-72@2x.png" width="144" height="144"/>
        <!-- iPhone Spotlight and Settings Icon -->
        <icon src="icon-splash/ios/icons/icon-small.png" width="29" height="29"/>
        <icon src="icon-splash/ios/icons/icon-small@2x.png" width="58" height="58"/>
        <!-- iPad Spotlight and Settings Icon -->
        <icon src="icon-splash/ios/icons/icon-50.png" width="50" height="50"/>
        <icon src="icon-splash/ios/icons/icon-50@2x.png" width="100" height="100"/>

        <!-- Config iOS Splash -->
        <splash src="icon-splash/ios/splashes/Default~iphone.png" width="320" height="480"/>
        <splash src="icon-splash/ios/splashes/Default@2x~iphone.png" width="640" height="960"/>
        <splash src="icon-splash/ios/splashes/Default-Portrait~ipad.png" width="768" height="1024"/>
        <splash src="icon-splash/ios/splashes/Default-Portrait@2x~ipad.png" width="1536" height="2048"/>
        <splash src="icon-splash/ios/splashes/Default-Landscape~ipad.png" width="1024" height="768"/>
        <splash src="icon-splash/ios/splashes/Default-Landscape@2x~ipad.png" width="2048" height="1536"/>
        <splash src="icon-splash/ios/splashes/Default-568h@2x~iphone.png" width="640" height="1136"/>
        <splash src="icon-splash/ios/splashes/Default-667h.png" width="750" height="1334"/>
        <splash src="icon-splash/ios/splashes/Default-736h.png" width="1242" height="2208"/>
        <splash src="icon-splash/ios/splashes/Default-Landscape-736h.png" width="2208" height="1242"/>
    </platform>
```
Cordova在添加平台或者构建的时候会根据此配置，将icon和splash复制到相应的平台中，见下图：
![cordova-android-icon-splash](http://zhoujianhui.bitbucket.org/cordova/cordova-android-icon-splash.png) ![cordova-ios-icon-splash](http://zhoujianhui.bitbucket.org/cordova/cordova-ios-icon-splash.png)

**PS**:对于Android平台有时会出现无法显示splash的情况，我们可以通过**cordova-plugin-splashscreen**插件解决。
安装完cordova-plugin-splashscreen后，在config.xml中配置splash的显示。
```XML
<preference name="SplashScreen" value="screen"/>
<preference name="SplashScreenDelay" value="5000"/>
```