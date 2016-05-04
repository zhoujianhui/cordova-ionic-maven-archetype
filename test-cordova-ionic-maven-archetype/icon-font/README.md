# icon-font
icon-font用于将svg格式的icons转换为iconfont字体格式

## Prepare
icon-font采用Gulp以及相应的Gulp任务完成转换。需要实现安装如下模块：
```
npm install gulp-cli -g
npm install gulp -g
npm install gulp-iconfont -g
npm install gulp-iconfont-css -g
```

## Usage
1、将所需生成字体的svg放置在icons下

2、修改配置文件iconfont-config.js，默认生成名为项目名称的字体并放置在项目的application/fonts下和名为项目名称的样式并放置在项目的application下

3、执行如下命令
```
gulp --gulpfile iconfont-config.js
```
为了方便使用我们提供Maven的Profile：**generate-iconfont** 执行上述命令

4、使用iconfont
在index.html中引入字体样式
```
<link rel="stylesheet" href="application/<PROJECT_NAME>.css">
```
使用字体图表
```html
<div class="icon icon-test">test iconfont</div>
```
**PS**: 发布时无需在发布代码index.html中引入字体样式，因为它会被打包进application.min.css中
