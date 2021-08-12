## 核心概念
- entry
- output
- loader
- plugin
- mode


### loader

2. 常见得loader
- css-loader  加载css
- ts-loader  ts
- sass-loader sass
- less-loader 
- style-loader 
- file-loader url-loader  image font
- babel-loader babel


loader 从右到左执行

3. loader 特性
- loader支持链式调用
- loader 可以是同步的，也可以是异步的

### plugin
1. webpack 插件是一个具有 apply 方法的 JavaScript 对象。apply 方法会被 webpack compiler 调用，并且在 整个 编译生命周期都可以访问 compiler 对象

2. 常见plugin
- HtmlWebpackPlugin Easily create HTML files to serve your bundles
- DllPlugin Split bundles in order to drastically improve build time
- CopyWebpackPlugin Copies individual files or entire directories to the build directory
- EslintWebpackPlugin A ESLint plugin for webpack
- ImageminWebpackPlugin  
- ClearWebpackPlugin
- UglifyWebpackPlugin
