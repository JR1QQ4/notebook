# Parcel 

```
cnpm init -y
cnpm install -g parcel-bundler

cnpm install --save-dev san @babel/core
```

创建 index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script src="./index.js"></script>
</body>
</html>
```

创建 index.js
```
import san from 'san';

var MyApp = san.defineComponent({
    template: '<p>Hello {{name}}!</p>',

    initData: function () {
        return {
            name: 'San'
        };
    }
});
var myApp = new MyApp();
myApp.attach(document.body);
```

配置 package.json
"build": "parcel build index.html -d build --public-url ./"
```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "parcel index.html",
    "dev": "parcel index.html",
    "build": "parcel build index.html -d build/output"  // 指定特定的路径
  }
```

运行
```
cnpm run start
cnpm run dev
cnpm run dev
```
