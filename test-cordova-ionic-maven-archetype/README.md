#test-cordova-ionic-archetype
Cordova + Ionic hybrid app created from cordova-ionic-archetype


##项目的结构(Project Layout) - 种子的基因
本项目除了业务代码部分，还提供了多种开箱即用的解决方案。

![项目结构](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-layout.png)

###icon-font
Ionic自定义样式需要用到字体图片资源，icon-font用于将svg格式的icons转换为iconfont字体格式。
详见：[icon-font/README.md](icon-font/README.md)

###icon-splash
项目发布时需要为每个平台生成对应的一系列Icon和Splash,为此我们使用NodeJS开发**cordova-icon-splash**,它会根据配置文件自动生成所需的图片资源。
详见：[icon-splash/README.md](icon-splash/README.md)

###init
init用于初始化Cordova项目。目前仅用于自动化安装Cordova的平台和插件，因为平台和插件不是我们开发的，所以不能纳入版本控制。那么当发生变化时，如组员安装了一个新的插件，其他人能通过初始化工具自动安装此插件，而不是更新代码。为此我们用NodeJS开发了**cordova-init**，它会根据配置文件初始化（添加/删除）平台和插件。
详见：[init/README.md](init/README.md)

###localization
项目有时需要根据手机的语言设置显示不同语言的界面，这个叫做**Localization**。localization用于项目的国际化，我们使用NodeJS开发**cordova-localize**完成此功能。
详见：[localization/README.md](localization/README.md)

###release
项目的发布包括发布代码、构建和部署。
详见：[release/README.md](release/README.md)

###scss
利用scss开发css,目前用于自定义Ionic样式

###www
包含按业务领域组织,模块化开发的业务项目代码，开发过程见《发布业务项目/收获》

###.gitignore
我们推荐使用分布式版本控制Git，.gitignore用于标注哪些文件不纳入版本控制

###.svnignore
兼顾使用SVN的团队

###config.xml
Cordova的配置文件

###pom.xml
Maven的配置文件，我们采用多配置(Multiple Profiles)的方式，自定义多个构建过程：  
![Maven多配置](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-multiple-profiles.png)    
具体使用参见《运行业务项目/检查种子质量》《发布业务项目/收获》章节

###README.md
项目自描述文件，采用Markdown的语法，记录项目**基因**


##运行业务项目 - 检查种子质量
此时生成的业务项目是一个**完整可运行**的Cordova项目。下面我们介绍如何运行这个业务项目。

###添加平台和插件
上文我们介绍了手工命令来安装平台和插件，这里我们推荐Maven Plugin的方式来执行。
我们的多配置中**init-platforms**和**init-plugins**分别用于安装平台和插件，只需勾选执行即可。  
![Maven执行项目初始化](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-init.png)   

当然也可以通过Maven命令执行:
```
mvn package -P init-platforms,init-plugins
```

添加平台后，如果安装新的插件，可在**init/init-config.json**中配置插件信息，然后执行：
```
mvn package -P init-plugins
```

###运行项目
开发阶段我们推荐使用模拟器运行项目，没有问题后再安装到设备。
众所周知Android的模拟器启动异常缓慢，iOS的模拟器需要苹果电脑，而我们的项目使用Web技术栈开发移动应用，所以我们基于浏览器的模拟器[Apache Ripple](http://ripple.incubator.apache.org)
>Apache Ripple™ is a web based mobile environment simulator designed to enable rapid development of mobile web applications for various web application frameworks, such as Apache Cordova™ and BlackBerry® WebWorks™. 
>It can be paired with current web based mobile development workflows to decrease time spent developing and testing on real devices and/or simulators.

首先我们安装Apache Ripple，它属于NodeJS Module，通过NodeJS的模块管理器**npm**安装
```
npm install -g ripple-emulator
```

启动模拟器
```
ripple emulate
``` 
![Apache Ripple](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-ripple.png) 

**PS**:我们主要通过浏览器的开发者工具调试解决JS的错误


##开发业务项目 - 培育
这里包含了我们对现代Web开发总结的最佳实践及团队约定。

###管理依赖
我们按照如下分类组织：
- 主流框架或者库
- 主流框架或者库的扩展插件
- 针对具体领域的库
- Miscellaneous

我们的引入规则：
- 需要同时引入开发版js(\*.js)和发布版js(\*.min.js)。如果第三方库没有按照此规则的，请主动改名再引入。对于未提供发布版js的，请使用UglifyJS自行处理。
- 引入后请按规则写在README.md中：名称,官网首页,版本号,简介

####主流框架或者库
- [jquery](http://jquery.com): v2.2.0
- [Ionic](http://ionicframework.com): v1.2.4 其打包了：
    - [angularjs](https://angularjs.org/): v1.4.3 含angular-animate.js,angular-sanitize.js
    - [angular ui-router](https://github.com/angular-ui/ui-router): v0.2.13

####主流框架或者库的扩展插件
- [ngCordova](http://ngcordova.com/): v0.1.24-alpha
- [angular-local-storage](https://github.com/grevory/angular-local-storage): v0.2.7 An AngularJS module that gives you access to the browsers local storage with cookie fallback

###业务开发
我们遵循领域驱动的模块化开发模式，www下的每个文件夹都代表一个业务领域，文件夹以业务领域命名。

默认我们提供了如下的模块: 
- application: 应用主模块，负责应用的启动，提供本地会话，模块未发布（未找到）时的提醒功能
- dummy: 可选的虚拟模块，用于示例模块是如何开发的
- home: 可选的首页模块，用于应用的导航
- login: 可选的登陆模块，用于示例用户登录
- \<appName\>.js: 应用的配置文件，用于配置加载的模块和全局的属性配置，如后端服务地址

开发新模块的步骤需要掌握AngularJS及UI-Router，不在本文讨论范围内。

下面以dummy为例，加以说明: 

1. 新建模块文件夹并按业务领域命名为dummy
2. 新建模块状态机dummy.js,利用AngularJS UI-Router描述模块内部的页面路由
3. 按照状态机新建模版文件dummy.html,即页面
4. 按照状态机新建控制器文件dummy.controller.js,用于处理业务逻辑
5. 利用依赖注入挂载模块
    * 在<appName>.js中注入模块：
      ```
      angular.module("<appName>", ["<appName>.dummy"])
      ```
    * 在index.js中引用dummy.js和dummy.controller.js
6. 在home.html中添加dummy模块的导航： 
   ```
   <div ui-sref="dummy">Dummy模块</div>
   ```


##发布业务项目 - 收获
我们认为发布应该包括三部分：
- build: 构建，此处我们包含android、ios构建相关的配置和web资源优化的配置
- deploy：部署，此处包含ios发布到App Store的配置
- code：发布代码，区别于开发代码，比如生产环境下的后端服务地址

具体的发布过程如下：

1. 在pom.xml中**releaseModules**属性中指定要发布的模块名
2. 在release/build/web/wro.xml中配置发布模块的资源优化（建议配置全模块，因为构建是根据releaseModules优化指定模块的）
3. 在release/code中的<appName>.js中注入模块名，在\<appName\>.js中引用优化后的资源：\<moduleName\>.min.js和\<moduleName\>.min.css
4. 按需构建android或者ios,你只需勾选相应的构建Profile

   ![Build Android](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-build-android.png)
5. 构建完了之后会在**target**下生成<appName>.apk。为了测试，我们提供了基于蒲公英的OTA方式供测试人员扫码下载

   ![Deploy Android APP To Pgyer](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-deploy-android-app-to-pgyer.png)

对于ios我们分别提供了AdHoc和AppStore两种构建和部署方式：

![Build And Deploy iOS AdHoc App](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-build-and-deploy-ios-adhoc-app.png)                    ![Build And Deploy iOS AppStore App](http://zhoujianhui.bitbucket.org/cordova/cordova-ionic-archetype-build-and-deploy-ios-appstore-app.png)
