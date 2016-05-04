#cordova-localize
cordova-localize用于为平台添加国际化和本地化资源，目前只做到文字资源的国际化，icon和splash的国际化有待开发。
此工具的初衷是解决ios开发时，需要XCode手工配置国际化，且较繁复。

*PS*: 因为Cordova打包成APP时的文件名称和显示名称均来自config.xml中name的配置，而我们希望安装文件名为英文，显示名称国际化，所以目前我们的国际化资源文件中只包含了APP在HomeScreen中的显示名称。

##Usage
1、新建文件夹localization，用于存放配置文件和资源文件

2、cordova-localize默认配置文件为**localization-config.json**，用于配置各平台支持的语言。
默认添加如下：
```JSON
{
  "android": [
    "en",
    "zh"
  ],
  "ios": [
    "en",
    "zh-Hans"
  ]
}
```


3、在localization中建立各平台的国际化资源

![cordova-localization](http://zhoujianhui.bitbucket.org/cordova/cordova-localization.png)

- android资源位于values-<language>/strings.xml中
``` XML
  <?xml version="1.0" encoding="utf-8"?>
  <resources>
      <string name="app_name">YOUR_APP_NAME</string>
      <string name="launcher_name">@string/app_name</string>
      <string name="activity_name">@string/launcher_name</string>
  </resources>
```
- ios资源位于<language>.lproj/InfoPlist.strings中
```
CFBundleDisplayName="YOUR_APP_NAME";
```


4、安装cordova-localize：
```
npm install cordova-localize -g
```
执行：
```
cd icon-localize
cordova-localize
```