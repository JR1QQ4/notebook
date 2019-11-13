# webpack 

webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。

从 webpack v4.0.0 开始，可以不用引入一个配置文件。然而，webpack 仍然还是高度可配置的。在开始前你需要先理解四个核心概念：

+ 入口(entry)
+ 输出(output)
+ loader
+ 插件(plugins)

### 入口(entry)

入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

可以通过在 webpack 配置中配置 entry 属性，来指定一个入口起点（或多个入口起点）。默认值为 ./src。

1.单个入口（简写）语法

用法：`entry: string|Array<string>`

```
// webpack.config.js
const config = {
  entry: './path/to/my/entry/file.js'
};
module.exports = config;
```

entry 属性的单个入口语法，是下面的简写：
```
const config = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
}; // 向 entry 传入「文件路径(file path)数组」将创建“多个主入口(multi-main entry)”
```

2.对象语法

用法：`entry: {[entryChunkName: string]: string|Array<string>}`

```
// webpack.config.js
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};  // “可扩展的 webpack 配置”是指，可重用并且可以与其他配置组合使用
```

3.常见场景

```
const config = {  // 分离 应用程序(app) 和 第三方库(vendor) 入口
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};

const config = {   // 多页面应用程序
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```


### 出口(output)

output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist。

1.用法

在 webpack 中配置 output 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

-  `filename` 用于输出文件的文件名。
-  目标输出目录 `path` 的绝对路径。

```
// webpack.config.js
const path = require('path');  // path 模块是 Node.js 的模块用于操作文件路径的
module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};

{   // 多个入口起点
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
}   // 写入到硬盘：./dist/app.js, ./dist/search.js

output: {   // 使用 CDN 和资源 hash 
  path: "/home/proj/cdn/assets/[hash]",
  publicPath: "http://cdn.example.com/assets/[hash]/"
}  
// 在编译时不知道最终输出文件的 publicPath 的情况下，publicPath 可以留空
// 并且在入口起点文件运行时动态设置。如果你在编译时不知道 publicPath，
// 你可以先忽略它，并且在入口起点设置 __webpack_public_path__。
__webpack_public_path__ = myRuntimePublicPath
```

### loader

loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 能够 import 导入任何类型的模块（例如 .css 文件）。

首先安装相对应的 loader：
```
npm install --save-dev css-loader
npm install --save-dev ts-loader
```

然后指示 webpack 对每个 .css 使用 css-loader，以及对所有 .ts 文件使用 ts-loader：
```
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```

在更高层面，在 webpack 的配置中 loader 有两个目标：

- test 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件。
- use 属性，表示进行转换时，应该使用哪个 loader。

```
// webpack.config.js
const path = require('path');
const config = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  }, // 在 webpack 配置中定义 loader 时，要定义在 module.rules 中，而不是 rules
  module: {
    rules: [  
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }   // 碰到「在 require()/import 语句中被解析为 '.txt' 的路径」时
};  // 在你对它打包之前，先使用 raw-loader 转换一下
module.exports = config;
```

在你的应用程序中，有三种使用 loader 的方式：

- 配置（推荐）：在 webpack.config.js 文件中指定 loader。
- 内联：在每个 import 语句中显式指定 loader
- CLI：在 shell 命令中指定它们。

```
module: {  // 配置[Configuration]
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
}

import Styles from 'style-loader!css-loader?modules!./styles.css';  // 内联

webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```

### 插件(plugins)

loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。

想要使用一个插件，你只需要 require() 它，然后把它添加到 plugins 数组中。多数插件可以通过选项(option)自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用 new 操作符来创建它的一个实例。
```
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件
const path = require('path');
const config = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
module.exports = config;
```

webpack 插件是一个具有 apply 属性的 JavaScript 对象。apply 属性会被 webpack compiler 调用，并且 compiler 对象可在整个编译生命周期访问。
```
// ConsoleLogOnBuildWebpackPlugin.js
const pluginName = 'ConsoleLogOnBuildWebpackPlugin';
class ConsoleLogOnBuildWebpackPlugin {
    apply(compiler) {
        compiler.hooks.run.tap(pluginName, compilation => {
            console.log("webpack 构建过程开始！");
        });
    }
}
```

### 模式(mode)

通过选择 development 或 production 之中的一个，来设置 mode 参数，你可以启用相应模式下的 webpack 内置的优化。
```
module.exports = {
  mode: 'production'
};
```

-  development ： 会将 `process.env.NODE_ENV` 的值设为 `development`。启用 `NamedChunksPlugin` 和 `NamedModulesPlugin`。
-  production ： 会将 `process.env.NODE_ENV` 的值设为 `production`。启用 `FlagDependencyUsagePlugin`, `FlagIncludedChunksPlugin`, `ModuleConcatenationPlugin`, `NoEmitOnErrorsPlugin`, `OccurrenceOrderPlugin`, `SideEffectsFlagPlugin` 和 `UglifyJsPlugin`.

只设置 `NODE_ENV`，则不会自动设置 `mode`。

### 配置(configuration)

webpack 的配置文件，是导出一个对象的 JavaScript 文件。此对象，由 webpack 根据对象定义的属性进行解析。

webpack 配置是标准的 Node.js CommonJS 模块，你可以做到以下事情：

-  通过 require(...) 导入其他文件
-  通过 require(...) 使用 npm 的工具函数
-  使用 JavaScript 控制流表达式，例如 ?: 操作符
-  对常用值使用常量或变量
-  编写并执行函数来生成部分配置

```
//  webpack.config.js
var path = require('path');  // 将路径或路径片段的序列解析为绝对路径
module.exports = {  // 基本配置
  mode: 'development',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js'
  }
};
```

### 模块(modules)

在模块化编程中，开发者将程序分解成离散功能块(discrete chunks of functionality)，并称之为模块。

### 模块解析(module resolution)

使用 `enhanced-resolve`，webpack 能够解析三种文件路径：

- 绝对路径：`import "C:\\Users\\me\\file";`、`import "/home/me/file";`
- 相对路径：`import "../src/file1";`、`import "./file2";`
- 模块路径：`import "module";`、`import "module/lib/file";`

### 构建目标(targets)

要设置 `target` 属性，只需要在你的 webpack 配置中设置 target 的值。
```
module.exports = {
  target: 'node'
};

var path = require('path');  // 多个 Target
var serverConfig = {
  target: 'node',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.node.js'
  }
};
var clientConfig = {
  target: 'web', // <=== 默认是 'web'，可省略
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.js'
  }
};
module.exports = [ serverConfig, clientConfig ];
```

## 入门实践

### 安装

1.安装

安装 webpack 之前需要安装 Node.js ，最好是使用 Node.js 最新的长期支持版本(LTS - Long Term Support)。安装完成后，需要新建一个文件夹，用来处理项目。

本地安装可以有几种不同的选择
```
npm install --save-dev webpack   # 安装最新版本
npm install --save-dev webpack@<version>  # 安装特定版本
npm install --save-dev webpack-cli  # 如果使用 webpack 4+ 版本，需要安装 CLI
```

也可以全局安装
```
npm install --global webpack
```

基本安装步骤
```
mkdir MyWebpack && cd MyWebpack   # 首先创建一个文件夹，并用cmd进入到该目录
npm init -y    # 初始化 npm
npm install webpack webpack-cli --save-dev  # 安装最新版本，并安装 CLI
```

2.创建项目文件夹和文件

```
  MyWebpack
  |- node_modules
  |- package.json
  |- package-lock.json
+ |- /dist  # “分发”代码，构建过程产生的代码优化后的“输出”目录，最终将在浏览器中加载
+   |- index.html
+ |- /src  # “源”代码，用于书写和编辑的代码
+   |- index.js
```

需要修改 package.json 文件：
```
{
    ...
+   "private": true,      # 确保安装包是私有的(private)
-   "main": "index.js",   # 移除 main 入口，防止意外发布你的代码
    ...
}
```

注意：包安装

-  npm install --save：在安装一个要打包到生产环境的安装包时使用
-  npm install --save-dev：在安装一个用于开发环境的安装包时使用

4.添加的内容

```
// dist/index.html
<!doctype html>
<html>
<head>
    <title>起步</title>
</head>
<body>
    <script src="main.js"></script>
</body>
</html>

// src/index.js   需要安装 lodash，npm install --save lodash
import _ from 'lodash';  # 引入的 lodash ，用于识别 _ ,
function component() {
    var element = document.createElement('div');
    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    return element;
}
document.body.appendChild(component());
```

5.执行 `npx webpack`，会将我们的脚本作为`入口起点`，然后 `输出` 为 `main.js`。或者使用命令`node_modules\.bin\webpack `。用浏览器打开 index.html 文件，可以查看到结果。

6.使用配置文件

```
  MyWebpack
  |- package.json
  |- webpack.config.js   # 配置文件
  |- /dist
    |- index.html
  |- /src
    |- index.js
```

webpack.config.js 内容：

```
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',   // 生成一个 ./dist/bundle.js 文件
    path: path.resolve(__dirname, 'dist')
  }
};
```

然后再次构建：`npx webpack --config webpack.config.js`，构建之后可以把 `index.html`文件中的 script 引用改为 `<script src="bundle.js"></script>`，删除 `main.js`浏览器能正常显示。

7.设置 NPM 脚本(NPM Scripts)

在 package.json 中添加：

```
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
+     "build": "webpack"
    }
```

添加之后，可以使用 `npm run build` 命令，来替代我们之前使用的 `npx` 命令。通过向 `npm run build` 命令和你的参数之间添加两个中横线，可以将自定义参数传递给 webpack，例如：`npm run build -- --colors`。

8.根据上面步骤，完成了 webpack 的基本配置，当前的目录结构：

```
  MyWebpack
  |- package.json
  |- webpack.config.js 
  |- /dist
    |- index.html
    |- bundle.js
  |- /src
    |- index.js
```


## 使用 webpack 搭建一个开发环境

1.支持 js、css 格式的解析

安装依赖：`npm install --save-dev style-loader css-loader`

```
 const path = require('path');

  module.exports = {
    mode: 'production',   // 压缩输出
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
+   module: {
+     rules: [
+       {
+         test: /\.css$/,
+         use: [
+           'style-loader',
+           'css-loader'
+         ]
+       }
+     ]
+   }
  };
```

在项目中添加一个新的 style.css 文件，内容比如为 `.hello { color:red; }`，`index.js` 中要使用这个 css，需要先导入：

```
+  import './style.css';  // 导入

+   element.classList.add('hello');  // 使用
```

此时工作目录：

```
  MyWebpack
  |- package.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
  |- /src
+   |- style.css
    |- index.js
  |- /node_modules
```

2.区分 development / production 环境

开发环境(development)和生产环境(production)的构建目标差异很大。在开发环境中，我们需要具有强大的、具有实时重新加载(live reloading)或热模块替换(hot module replacement)能力的 source map 和 localhost server。

在生产环境中，我们的目标则转向于关注更小的 bundle，更轻量的 source map，以及更优化的资源，以改善加载时间。由于要遵循逻辑分离，我们通常建议为每个环境编写彼此独立的 webpack 配置。

虽然，以上我们将生产环境和开发环境做了略微区分，但是，请注意，我们还是会遵循不重复原则(Don't repeat yourself - DRY)，保留一个“通用”配置。为了将这些配置合并在一起，我们将使用一个名为 `webpack-merge` 的工具。通过“通用”配置，我们不必在环境特定(environment-specific)的配置中重复代码。

安装 `webpack-merge`将代码分离：`npm install --save-dev webpack-merge`

分离之后的目录结构：

```
  MyWebpack
  |- package.json
+ |- webpack.common.js
+ |- webpack.dev.js
+ |- webpack.prod.js
  |- /dist
  |- /src
    |- index.js
  |- /node_modules
```

webpack.common.js

```
+ const path = require('path');
+ module.exports = {
+   entry: {
+     app: './src/index.js'
+   },
+   output: {
+     filename: '[name].bundle.js',
+     path: path.resolve(__dirname, 'dist')
+   }
+ };
```

webpack.dev.js

```
+ const merge = require('webpack-merge');
+ const common = require('./webpack.common.js');
+
+ module.exports = merge(common, {
+   devtool: 'inline-source-map',  // 更容易地追踪错误和警告，不要用于生产环境
+   devServer: {
+     contentBase: './dist'
+   }
+ });
```

webpack.prod.js：`uglifyjs-webpack-plugin` 用来缩小JavaScript，安装`$ npm install uglifyjs-webpack-plugin --save-dev`

```
+ const webpack = require('webpack');
+ const merge = require('webpack-merge');
+ const UglifyJSPlugin = require('uglifyjs-webpack-plugin');
+ const common = require('./webpack.common.js');
+
+ module.exports = merge(common, {
+   devtool: 'source-map',  // 更容易地追踪错误和警告
+   plugins: [
+     new UglifyJSPlugin({
+       sourceMap: true
+     }),
+     new webpack.DefinePlugin({
+       'process.env.NODE_ENV': JSON.stringify('production')  // 指定环境
+     })
+   ]
+ });
```

package.json

```
    "scripts": {
+     "start": "webpack-dev-server --open --config webpack.dev.js",
+     "build": "webpack --config webpack.prod.js"
    }
```

src/index.js

```
+ if (process.env.NODE_ENV !== 'production') {
+   console.log('Looks like we are in development mode!');
+ }  // 检查 /src 的本地代码都可以关联到 process.env.NODE_ENV 环境变量
```

3.使用npm scripts设罝dev、test、build命令

npm 允许在package.json文件里面，使用scripts字段定义脚本命令。

```
{
  "scripts": {
    "build": "node build.js"  // build命令对应的脚本是node build.js
  }
}
```

设置之后使用npm run命令，就可以执行这段脚本：`$ npm run build` 等同于 `$ node build.js`。

使用不带参数的`npm run`,显示`package.json`里所有的script脚本命令及内容。

每当执行`npm run`，就会自动新建一个 Shell，会将当前目录的`node_modules/.bin`子目录加入`PATH`变量，执行结束后，再将`PATH`变量恢复原样。

```
"test": "mocha test"  // 正确，当前目录的node_modules/.bin子目录里面的不必加上路径

"test": "./node_modules/.bin/mocha test"  // 错误
```

npm 执行顺序：

```
$ npm run script1.js & npm run script2.js  // 并行执行

$ npm run script1.js && npm run script2.js  // 继发执行
```

配置：

```
{
  "name": "MyWebpack",  // 当前目录名称
  "version": "1.0.0",  // 永远 1.0.0
  "description": "",  // 自述文件中的信息或空字符串 ""
  "main": "index.js",  // 永远 index.js
  "scripts": {  // 默认情况下会创建一个空test脚本
    "test": "echo \"Error: no test specified\" && exit 1", // npm run test
    "dev": "node build/dev-server.js", // ”npm run dev”执行build/dev-server.js
    "build": "node build/build.js", // ”npm run build”执行build/build.js文件
    "start": "node server.js"，  // npm run start的默认值是node server.js
    "install": "node-gyp rebuild" // npm run install的默认值是node-gyp rebuild
  },
  "keywords": [],  // 关键字
  "author": "",  // 作者
  "license": "ISC",  // ISC License
  "devDependencies": {  // 这些包仅用于开发和测试
    "css-loader": "^3.0.0",
    "extract-text-webpack-plugin": "^3.0.2",
    "style-loader": "^0.23.1",
    "webpack": "^4.35.2",
    "webpack-cli": "^3.3.5",
    "webpack-dev-server": "^3.7.2",
    "webpack-merge": "^4.2.1"
  },
  "dependencies": {  // 您的应用程序在生产中需要这些包
    "lodash": "^4.17.11"
  }
}
```

4.写一个san组件并在浏览器中显示hello world

新建一个文件夹 san，用 cmd 进入文件夹，安装模块和依赖：

```
cnpm install --save san san-router   
cnpm install --save-dev html-webpack-plugin style-loader css-loader babel-loader san-loader webpack-dev-server webpack-cli webpack html-loader @babel/core
```

此时 package.json 文件内容：

```
{
  "name": "san",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.5.0",
    "babel-loader": "^8.0.6",
    "css-loader": "^3.0.0",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "san-loader": "^0.0.7",
    "style-loader": "^0.23.1",
    "webpack": "^4.35.2",
    "webpack-cli": "^3.3.5",
    "webpack-dev-server": "^3.7.2"
  },
  "dependencies": {
    "san": "^3.7.7",
    "san-router": "^1.2.1"
  }
}
```

在根目录创建 index.html：

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>san-app</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

创建文件夹 src，然后在这个文件夹下创建 index.js 和 hello.san ：

hello.san

```
<template>
    <div class="hello">hello {{msg}}</div>
</template>
<script>
    export default {
        initData () {
            return {
                msg: 'world'
            };
        }
    }
</script>
<style>
    .hello {
        color: blue;
    }
</style>
```

index.js

```
import san from 'san';
import {router} from 'san-router'
import Hello from './Hello.san'
router.add({rule: '/', Component: Hello, target: '#app'})
router.start()
```

创建 webpack.config.js 用于配置文件关系：

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
entry: './src/index.js',
output: {
  filename: 'bundle.js',
  path: path.resolve(__dirname, 'dist')
},
module: {
 rules: [
   {
     test: /\.css$/,
     use: [
       'style-loader',
       'css-loader'
     ]
   },
   {
       test: /\.js$/,
       use: 'babel-loader',
       exclude: /node_modules/
   },
    {
        test: /\.san$/,
        use: 'san-loader'
    },
 ]
},
plugins: [
  new HtmlWebpackPlugin({
      title: 'Output Management',
      template: 'index.html'
  })        
]
};
```

最后需要在 package.json 中设置一下启动脚本命令：

```
{
  ...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
+   "build": "webpack --config webpack.config.js",   
+   "start": "webpack-dev-server --open --config webpack.config.js"
  },
  ...
}
```

在 cmd 中运行 `npm run start`开启这个应用，运行`npm run build`打包这个应用，会在 dist 目录下生成 bundle.js 和 index.html 。

最终目录结构：

```
  san
  |- package.json  // npm init -y 生成的
  |- webpack.config.js  // 创建的配置文件
  |- index.html  // 创建的模板
  |- /dist  // 创建的文件夹
    |- bundle.js  // 打包生成的
    |- index.html  // html-webpack-plugin 插件生成的
  |- /src  // 创建的
    |- index.js  // 创建的
    |- hello.san  // 创建的
  |- /node_modules  // 安装模块生成的
```

如果 npm 失败，可能是网络问题，可以使用淘宝的npm：

```
 npm install -g cnpm --registry=https://registry.npm.taobao.org
```

[npm 中文文档](https://www.npmjs.cn/)
[npm scripts 使用指南](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)
[webpack中文文档](https://www.webpackjs.com/concepts/)
