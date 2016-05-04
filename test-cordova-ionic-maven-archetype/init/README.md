#cordova-init
cordova-init根据配置文件初始化（添加/删除）Cordova项目的平台和插件。

##Usage
1、新建文件夹init，用于存放配置文件。

2、cordova-init默认配置文件为**init-config.json**，用于配置平台和插件列表。默认提供如下的平台和插件：
```JSON
{
  "platforms": [
    "android",
    "ios"
  ],
  "plugins": [
    "cordova-plugin-whitelist",
    "cordova-plugin-splashscreen"
  ]
}
```
如果插件发布到npm库，那么只需要配置插件ID，否则需要插件在GitHub上的URL或者插件下载后所在的目录。
``` JSON
{
  ...
  "plugins": [
    "cordova-plugin-whitelist",
     {
          "id": "PLUGIN_ID",
          ["giturl":"https://github.com/xxx/xxx.git" || "directory":"DOWNLOADED_PLUGIN_PATH_"]
     }
  ]
}
```
同时插件也支持带参数的安装，如：
``` JSON
{
  ...
  "plugins": [
    "cordova-plugin-whitelist",
     {
          "id": "cordova-plugin-wechat",
          "variables": {
            "wechatappid": "YOUR_APPID"
          }
     }
  ]
}
```

*PS*:虽然cordova-plugin-whitelist在初始化平台的时候默认安装，但是我们还是希望显式的记录插件列表。如果你不需要某个平台或者插件，可以直接从配置中删除，执行命令后，对应的平台和插件也会从项目中删除。

3、安装cordova-init：
```
npm install cordova-init -g
```
初始化平台：
```
cd init
cordova-init -t/--target platform
```
初始化插件：
```
cd init
cordova-init -t/--target plugin
```