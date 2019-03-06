# webpack4-vue-demo
webpack4项目

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