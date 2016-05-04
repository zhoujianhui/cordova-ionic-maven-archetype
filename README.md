# cordova-ionic-maven-archetype
本原型由maven-archetype-archetype快速生成而来，用于快速开发基于Cordova+Ionic的Hybrid App

##设计理念(Design Philosophy)
**种子项目(Seed Project)** 来源于日常的项目开发，它内置代码资产、技术理念和团队文化，用于后续一类项目的快速开发，也可用于孵化开发平台和产品。
他的宗旨是**资产化(Asset)**: 产出可持续交付客户价值的模式、解决方案和利好团队战斗力的文化，而不仅是一堆应付的代码。
为此我们需要如下的技术和理念的支持：

- Development: OOP&A, SOLID+Patterns+Simple Design
- Infrastructure: VCS, BAS
- Team Process: Agile/Lean, Team Dynamics, Continuous Learning

##特性(Features)
目前我们采用Maven Archetype的方式来开发种子项目，种子项目**cordova-ionic-archetype**具有如下**特性(Features)** : 

- 拥抱领域驱动开发，支持按领域模块化的分析、开发、交付和维护
    - 支持模块热插拔
    - 内置通用模块(Cross Cutting Modules)，如登录
    - ...
- 完美集成现代Web开发和移动App开发    
    - 满足现代Web开发的要求
        - 支持以状态机的方式组合业务模块
        - 支持依赖注入业务模块和细粒度的服务
        - 支持Web资源的优化，如JS,CSS的压缩合并，HTML的压缩等
        - ...
    - 满足移动App开发的过程
        - 支持Android自动生成密钥文件、自动签名、ZipAlign
        - 支持iOS自动签名
        - 支持OTA，自动发布到蒲公英(http://www.pgyer.com) ，可通过扫码下载App
          此特性主要便于iOS应用真机测试时，在不越狱的情况下安装难的问题
        - ...  
    - 支持几乎零成本移植为微信公众平台项目 
- 发布是开发出来的，而不是手工重复劳动
    - 开发代码和发布代码分离
    - 支持以Maven Plugin和NodeJS自动化发布过程
    - ...

---

下面我们以种子从播种、培育、收获的过程形象的介绍如何基于种子项目开发业务项目
##通过种子项目生成业务项目 - 播种
cordova生成项目的命令如下：
```
cordova create <PATH> [ID [NAME [CONFIG]]]
```

现在我们使用maven archetype命令：
```
mvn archetype:generate 
-DarchetypeGroupId=org.zhoujianhui.archetypes
-DarchetypeArtifactId=cordova-ionic-maven-archetype
-DarchetypeVersion=0.0.1-SNAPSHOT
-DinteractiveMode=false 
-DgroupId=org.zhoujianhui
-DartifactId=test-cordova-ionic-maven-archetype 
-Dversion=0.0.1-SNAPSHOT 
[-DappId=org.zhoujianhui.testcordovaionicarchetype] 
[-DappName=test-cordova-ionic-archetype]
```

对比来看：

- PATH=artifactId,生成项目所在的目录
- ID=appId,应用的ID (Reverse-domain-style package name - used in config.xml's <widget id>)
- NAME=appName,应用的名称（Human readable name - used in config.xml's <widget name>）

其中[]表示可选，默认值为：

- appId=groupId.artifactId.replace("-","")，不能包含"-"
- appName=artifactId

**PS:**
为了避免通过原型生成项目耗时较长的问题（有可能是从公网遍历所有的原型导致）
第一次执行时，可添加archetypeCatalog参数指向原型所在的Nexus私服id（见Maven的settings.xml）
```
-DarchetypeCatalog=nexus
```

第二次执行时，可将archetypeCatalog参数指定为local，因为第一次已将原型下载到Maven的本地库
```
-DarchetypeCatalog=local
```

##种子项目的培育和收获
种子项目的培育和收获除了种子内置基因以外还和具体的业务项目相关，故此过程在业务项目的[README.md](test-cordova-ionic-maven-archetype/README.md)介绍。
