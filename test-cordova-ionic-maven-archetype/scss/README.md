#scss
scss简单来说是通过编程的方式生成css。我们采用**node-sass**将scss编译为css。
目前我们用于自定义Ionic的样式。

## 安装node-sass
```
npm install -g node-sass
```

##Custom Ionic
自定义Ionic样式，我们只需要在**application.ionic.scss**中覆写**\_variables.scss**中的变量即可。
执行：
```
 scss/ionic/application.ionic.scss www/application/application.ionic.css
```