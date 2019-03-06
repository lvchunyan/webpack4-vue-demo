# webpack4-vue-demo
webpack4项目

注：提交代码时报错（git提交node-modules报文件名过长无法提交问题）

fatal: unable to stat 'node_modules/gulp-connect/node_modules/gulp-util/node_modules/dateformat/node_modules/meow/node_modules/normalize-package-data/node_modules/validate-npm-package-license/node_modules/spdx-expression-parse/parser.generated.js': Filename too long

在.gitignore文件中忽略node-modules文件

步骤:
> 1.新建文件夹

> 2.安装依赖（命令行工具进入文件夹）

- （1）初始化
     
      cnpm init  //初始化
      
- （2）安装webpack webpack-cli
 
      cnpm i webpack webpack-cli -D   //i 是install的简写，-D 是 --save-dev的简写
   
- （3）在根目录创建index.html

       <!DOCTYPE html>
       <html lang="en">
       <head>
           <meta charset="UTF-8">
           <title>webpack4-vue-demo</title>
       </head>
       <body>
           <div id="root"></div>
       </body>
       </html>  
![工程目录](https://upload-images.jianshu.io/upload_images/12642255-583727756e84c187.png)

- (5)进行第一次打包(命令行输入)

       webpack

打包成功，结果如图:       
![](https://upload-images.jianshu.io/upload_images/12642255-2e1421dde8e55b83.png) 
       
       注意有个warning,意思是需要设定模式，如果不设定模式，默认为生产模式，生产模式是会压缩js代码
       此时回头看工程目录，多了一个dist文件夹，webpack4在打包时默认入口文件为src目录下的index.js，输出地址为dist文件夹，文件为main.js
       修改index.html的代码，然后在浏览器中打开，并且打开控制台
      
       <!DOCTYPE html>
       <html lang="en">
       <head>
           <meta charset="UTF-8">
           <title>webpack4-vue-demo</title>
       </head>
       <body>
           <div id="root"></div>
           <script src="./dist/main.js"></script>
       </body>
       </html>
       可以看到控制台打印出了我们在index.js中写的内容:hello!webpack4-vue-demo!   
   
- (6)安装vue, vue-loader
       
       cnpm i vue vue-loader -D

- (7)在src下创建App.vue
       
       <template>
           <div>{{msg}}</div>
       </template>
       <script>
       export default{
           data(){
               return{
                   msg: 'hello! webpack4-vue-demo!'
               }
           }
       }
       </script>
       
- (8)修改index.js
       
       import Vue from 'vue'
       import App from './App.vue'
       
       new Vue({
           el: "#root",
           render:h=>h(App)
       })

- (9)第二次打包

![报错](https://upload-images.jianshu.io/upload_images/12642255-17d66345fc7e2877.png)

这是由于vue-loader需要以插件的形式引入,即使安装了，但是我们需要在webpack.config.js中配置

- (10)在根目录下创建webpack.config.js

      const path = require('path')
      const VueLoaderPlugin = require('vue-loader/lib/plugin')
       
      module.exports = {
        mode: 'development',
        module: {
          rules: [
            {
              test: /\.vue$/,
              loader: 'vue-loader'
            },
          ]
        },
        plugins: [
          new VueLoaderPlugin()
        ]
      }

- (11)第三次打包
      
      ERROR in ./src/App.vue
      Module Error (from ./node_modules/_vue-loader@15.7.0@vue-loader/lib/index.js):
      [vue-loader] vue-template-compiler must be installed as a peer dependency, or a compatible compiler implementation must be passed via options.
       @ ./src/index.js 2:0-27 6:16-19
      
      ERROR in ./src/App.vue
      Module build failed (from ./node_modules/_vue-loader@15.7.0@vue-loader/lib/index.js):
      TypeError: Cannot read property 'parseComponent' of undefined
          at parse (E:\workProject\webpack4-vue-demo\node_modules\_@vue_component-compiler-utils@2.6.0@@vue\component-compiler-utils\dist\parse.js:14:23)
          at Object.module.exports (E:\workProject\webpack4-vue-demo\node_modules\_vue-loader@15.7.0@vue-loader\lib\index.js:67:22)
       @ ./src/index.js 2:0-27 6:16-19
错误很明显了，没有vue-template-compiler，所以我们:cnpm i vue-template-compiler -D

- (12)第四次打包

![成功](https://upload-images.jianshu.io/upload_images/12642255-9bff1a5f635383e5.png)