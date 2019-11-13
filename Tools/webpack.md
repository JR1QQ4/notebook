# webpack

1.nrm，可以提供一些npm镜像地址，有淘宝的镜像。

```
// 全局安l
npm install nrm -g
// 查看镜像服务器资源
nrm ls
// 切换镜像服务器，选择从哪个地址下载
nrm use cnpm
// 安装包
npm i jquery -S / npm i jquery -D
```

2.普通打包

```
// 初始创建的文件和目录，以及npm init生成的文件，下载的包
|- dist
|- src
    |- css
    |- images
    |- js
    |- index.html
    |- main.js
|- package.json
|- package-lock.json
|- node_modules 

// 普通打包，要指定模式，如果要更改默认文件名，需要添加参数-o
> webpack .\src\main.js -o .\dist\bundle.js --mode development
```

3.监听文件改变，自动打包，需要安装`webpack-dev-server`

```
npm install webpack-dev-server -D

// 因为安装时这个包是安装到项目目录中的，不能在命令行中直接使用，不是全局的命令
// 需要在 package.json中进行配置："dev":"webpack-dev-server"
// 然后运行 npm run dev
// 注意：index.html 此时引用的 bundle.js 不再是 ./dist/bundle.js
// 而是以 /bundle.js，这个文件是存放在项目根路径中，但没有显示出来，是因为存放在内存中
// 然后需要更改引用路径
<script src="/bundle.js"></script> 

// 自定义，--open打开浏览器，--port端口号，--contentBase打开路径，--hot热替换
"dev":"webpack-dev-server --open --port 3000 --contentBase src --hot"

// 自定义第二种方式，在webpack.config.js中配置
const webpack = require('webpack');
devServer: {
    hot: true,
    contentBase: "./src",
    port: 3000,
    open: true
},
plugins: [
    new webpack.HotModuleReplacementPlugin()
]
```

注意：此时index.html是存放在硬盘里的，./bundle.js是存放在内存中的

3.html-webpack-plugin插件把index.html文件存放发内存中

```
// 安装
npm i html-webpack-plugin -D
// 配置
const HtmlWebpackPlugin = require('html-webpack-plugin');
plugins: [
    new HtmlWebpackPlugin({
        template: path.join(__dirname, "/src/index.html"),  // 模板
        filename: 'index.html'  // 在内存中生成的文件，默认名称index.html
        // filename可以修改，指定生成页面，然后需要在网址中输入对应的地址访问
    })
]
// 在生成的index.html中，默认会在body结束标签前面生成一个script标签，引用对应js文件
<script type="text/javascript" src="bundle.js"></script>
```

4.loader加载器

（1）css，png，url

```
// > cnpm i style-loader css-loader less-loader less sass-loader node-sass url-loader
{ test: /\.css$/, use: [{ loader: "style-loader" }, { loader: "css-loader" }] },
{ test: /\.less$/, use: [{ loader: "style-loader" }, { loader: "css-loader" }, { loader: "less-loader" }] },
{ test: /\.scss$/, use: [{ loader: "style-loader" }, { loader: "css-loader" }, { loader: "sass-loader" }] },
// 处理css中的url；假如图片大小9832，添加配置limit，小于9832会使用原来的名称，大于等于9832使用base64编码
// 当小于9832时，可以指定文件名，为了避免文件重复，可以使用hash命名
{ test: /\.(png|jpg|gif|bmp|jpeg)$/, use: [{ loader: "url-loader", options: { mimetype: 'image/png',limit:9831,name:`[hash:8]-[name].[ext]` } }] }
// url-loader 可以处理图标字体
{test:/\.(ttf|eot|svg|woff|woff2)$/,use:[{loader:"url-loader"}]}
```

（2）babel-loader

```
// 这是以前3.X的
第一套包：> cnpm i babel-core babel-loader babel-plugin-transform-runtime -D
第二套包：> cpm i babel-preset-env babel-preset-stage-0 -D  //babel语法包
// 排除 node_modules 中的第三方 js 文件
{test:/\.js$/,use:"babel-loader",exclude:/node_modules/}
// 创建配置文件 .babelrc
{ 
    "presets":["env","stage-0"], 
    "plugins":["transform-runtime"]
}

// 4.X
安装：> cnpm install -D babel-loader @babel/core @babel/preset-env
上面安装错误提示需要安装插件：> cnpm i @babel/plugin-proposal-class-properties -D

为了避免重复插入辅助代码：>cnpm install -D @babel/plugin-transform-runtime
但是提示找不到模块：>cnpm install --save @babel/runtime
{ test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
{
    "presets": [
        "@babel/preset-env"
    ],
    "plugins": [
        ["@babel/plugin-proposal-class-properties"],
        ["@babel/plugin-transform-runtime"]
    ]
}
```

5.vue

```
// 安装vue
> cnpm i -S vue
// 安装完成之后，查看vue的package.json文件，可以看到入口js不是vue.js
// 所以在导入包时，import Vue from "vue"执行不出正确的代码
// 需要引入 import Vue from "../node_modules/vue/dist/vue.js"
// 或者在 webpack.config.js中配置resolve
resolve: {
    alias: {
         vue$: "vue/dist/vue.js"
    }
}

// 为了能解析 .vue 文件名的文件，需要安装加载器
> npm install -D vue-loader vue-template-compiler
// 此时可以注释掉 resolve，直接 import Vue from "vue"
// 然后需要配置 webpack.config.js 文件
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module:{ rules:[ { test: /\.vue$/, loader: 'vue-loader' } ] }

plugins: [
    new VueLoaderPlugin()
]
```

6.export

```
node 导出： module.exports = {}  和  exports
     导入： var 名称 = require('模块标识符')

es6 导出： export default{ } 和 export
    导入： import 模块名称 from '模块标识符'

// 区别
export default 可以自定义接收的名称
export default 只能向外导出 1 次，export 可以向外暴露多次
export 导入的时候需要使用 花括号 接收，并且按需导入，想导入多少个就导入多少
export 导入可以使用 as 起别名

// index.js
var obj = { name: "zs", age: 23 }
export default obj
export var title = "xiaoming"
export var title2 = "xiaoming2"

// main.js
import myObj,{ title, title2 } from 'index.js'
import { title as xiaoming } from 'index.js'
```

7.vue-router

```
> cnpm i vue-router -S
import Vue from 'vue'
import VueRouter from 'vue-router'
import App from './vue/app.vue'
import About from './vue/about.vue'
import Contact from './vue/contact.vue'
import Login from './vue/contact/login.vue'
import Register from './vue/contact/register.vue'

Vue.use(VueRouter)

const router = new VueRouter({
    routes: [
        { path: "/about", component: About },
        {
            path: "/contact", component: Contact, children: [  // 子路由
                { path: "login", component: Login }, 
                { path: "register", component: Register }
            ]
        }
    ]
})

new Vue({
    el: "#app",
    render: c => c(App),
    router
})

// 路由中，设置私有 style 属性，添加 scoped，默认是全局样式
// style 可以使用 sass less，添加属性 lang="less" lang="sass" 
<style scoped>
    h1 {
        color: coral;
    }
</style>
```
