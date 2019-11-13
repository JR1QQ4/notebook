## HTML5 本地存储

1.LocalStorage
localStorage 类似 sessionStorage，但其区别在于：存储在 localStorage 的数据可以长期保留；而当页面会话结束——也就是说，当页面被关闭时，存储在 sessionStorage 的数据会被清除 。
```
localStorage.setItem('myCat', 'Tom');  // 添加
let cat = localStorage.getItem('myCat');  // 读取
localStorage.removeItem('myCat');  // 移除特定的
localStorage.clear();  // 移除所有

sessionStorage.setItem('key', 'value'); // 保存数据到 sessionStorage
let data = sessionStorage.getItem('key'); // 从 sessionStorage 获取数据
sessionStorage.removeItem('key'); // 从 sessionStorage 删除保存的数据
sessionStorage.clear(); // 从 sessionStorage 删除所有保存的数据
```

2.Cookie
当 web 服务器向浏览器发送 web 页面时，在连接关闭后，服务端不会记录用户的信息。Cookie 的作用就是用于解决 "如何记录客户端的用户信息"。
```
// 创建 cookie
document.cookie="username=John Doe";
// 添加一个过期时间（以 UTC 或 GMT 时间）
document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT";
// path 参数告诉浏览器 cookie 的路径
document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";

// 读取 Cookie，cookie1=value; cookie2=value;...
var x = document.cookie; 
// 修改 cookie 类似于创建 cookie
document.cookie="username=John Smith; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/"; 
// 删除 Cookie，设置 expires 参数为以前的时间即可
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";

function setCookie(cname,cvalue,exdays){ // 设置cookie
  var d = new Date(); // cname键，cvalue值，exdays过期时间
  d.setTime(d.getTime()+(exdays*24*60*60*1000));
  var expires = "expires="+d.toGMTString();
  document.cookie = cname + "=" + cvalue + "; " + expires;
}

function getCookie(cname){ // 获取cookie的值
  var name = cname + "=";
  var ca = document.cookie.split(';');
  for(var i=0; i<ca.length; i++) {
    var c = ca[i].trim();
    if (c.indexOf(name)==0) return c.substring(name.length,c.length);
  }
  return "";
}
```

3.Indexed Database API
- IndexedDB 是一个事务型数据库系统，类似于基于SQL的RDBMS。 IndexedDB允许您存储和检索用键索引的对象；可以存储结构化克隆算法支持的任何对象。
- 键值对储存、异步、支持事务...
[参考文档-浏览器数据库 IndexedDB 入门教程](http://www.ruanyifeng.com/blog/2018/07/indexeddb.html)
```
// 打开数据库,如果指定的数据库不存在，就会新建数据库
var request = window.indexedDB.open(databaseName, version); 
// request通过三种事件error、success、upgradeneeded，处理打开数据库的操作结果
    // 打开数据库失败
    request.onerror = function (event) { 
      console.log('数据库打开报错'); 
    };
    // 成功打开数据库
    var db;
    request.onsuccess = function (event) {
      db = request.result;
      console.log('数据库打开成功');
    };
    // 如果指定的版本号，大于数据库的实际版本号，就会发生数据库升级事件upgradeneeded
    request.onupgradeneeded = function(event) {
        var db;
        // 通过事件对象的target.result属性，拿到数据库实例
        db = event.target.result;
    };

// 新建数据库，新建数据库与打开数据库是同一个操作
// 新建表，在upgradeneeded事件里面完成，因为这时版本从无到有，所以会触发这个事件
request.onupgradeneeded = function(event) {
  var db = event.target.result;
  var objectStore;
  // 判断这张表格是否存在，如果不存在再新建
  if (!db.objectStoreNames.contains('person')) {
    // 创建表，指定主键
    objectStore = db.createObjectStore('person', { keyPath: 'id' });
    // 新建索引，引名称、索引所在的属性、配置对象
    objectStore.createIndex('name', 'name', { unique: false });
    objectStore.createIndex('email', 'email', { unique: true });
  }
}
    // 指定主键为一个递增的整数
    var objectStore = db.createObjectStore('person',{ autoIncrement: true });

// 新增数据需要通过事务完成，指定表格名称和操作模式（"只读"或"读写"）
function add() { 
  var request = db.transaction('person', 'readwrite')
    .objectStore('person') // 拿到 IDBObjectStore 对象，通过表格对象的add()添加
    .add({ id: 1, name: '张三', age: 24, email: 'zhangsan@example.com' }); 
  request.onsuccess = function (event) {
    console.log('数据写入成功');
  };
  request.onerror = function (event) {
    console.log('数据写入失败');
  }
}
add();

// 读取数据，通过事务完成
function read() {
   var transaction = db.transaction(['person']);
   var objectStore = transaction.objectStore('person');
   var request = objectStore.get(1); // 用于读取数据，参数是主键的值
   request.onerror = function(event) {
     console.log('事务失败');
   };
   request.onsuccess = function( event) {
      if (request.result) {
        console.log('Name: ' + request.result.name);
        console.log('Age: ' + request.result.age);
        console.log('Email: ' + request.result.email);
      } else {
        console.log('未获得数据记录');
      }
   };
}
read();

// 遍历数据，用指针对象 IDBCursor
function readAll() {
  var objectStore = db.transaction('person').objectStore('person');
   objectStore.openCursor().onsuccess = function (event) {
     var cursor = event.target.result;
     if (cursor) {
       console.log('Id: ' + cursor.key);
       console.log('Name: ' + cursor.value.name);
       console.log('Age: ' + cursor.value.age);
       console.log('Email: ' + cursor.value.email);
       cursor.continue();
    } else {
      console.log('没有更多数据了！');
    }
  };
}
readAll();

// 更新数据要使用IDBObject.put()方法
function update() {
  var request = db.transaction(['person'], 'readwrite')
    .objectStore('person')
    .put({ id: 1, name: '李四', age: 35, email: 'lisi@example.com' });
  request.onsuccess = function (event) {
    console.log('数据更新成功');
  };
  request.onerror = function (event) {
    console.log('数据更新失败');
  }
}
update();

// 删除数据，IDBObjectStore.delete()方法用于删除记录
function remove() {
  var request = db.transaction(['person'], 'readwrite')
    .objectStore('person')
    .delete(1);
  request.onsuccess = function (event) {
    console.log('数据删除成功');
  };
}
remove();

// 使用索引，可以搜索任意字段，如果不建立索引，默认只能搜索主键
var transaction = db.transaction(['person'], 'readonly');
var store = transaction.objectStore('person');
var index = store.index('name');
var request = index.get('李四');
request.onsuccess = function (e) {
  var result = e.target.result;
  if (result) {...} else {...}
}
```

4.FileSystem API
[参考文档 HTML5 本地文件操作之FileSystemAPI实例（一）](https://blog.csdn.net/weixin_33859844/article/details/85859657)
```
window.requestFileSystem = window.requestFileSystem || window.webkitRequestFileSystem;
window.webkitStorageInfo.requestQuota(window.PERSISTENT, 1024 * 1024 * 5, function (gratedBytes) {
    console.log('请求成功的空间：' + gratedBytes);
    window.requestFileSystem(window.PERSISTENT, gratedBytes, initFs, errorHandler);
}, errorHandler);
function initFs(fs) {
    fs.root.getFile('test1.txt', {
        create: true,  
        exclusive: true 
    }, function (fileEntry) {
        console.info(fileEntry);
        console.log('文件创建成功，' + fileEntry.name);
    }, errorHandler);
    fs.root.getDirectory('MyPictures', { create: true }, function (dirEntry) {
        dirEntry.getFile('log3.txt', { create: true }, function (fileEntry) {
            console.log('目录下文件创建成功：' + fileEntry.fullPath);
        }, errorHandler);
        dirEntry.getFile('test1.txt', { create: true }, function (fileEntry) {
            console.log('目录下文件创建成功：' + fileEntry.fullPath);
        }, errorHandler);
    }, errorHandler)
}
function errorHandler(err) {
    console.error(err);
    console.info('创建文件是失败');
}
```

5.Application Cache
[参考文档](https://blog.csdn.net/arvin0/article/details/51158836)
```
// 在index.html目录下，新建类似于cache.manifest的manifest文件并在index.html下的html标签内新增manifest属性
<!DOCTYPE HTML><html manifest = "cache.manifest">...</html>

// 配置该文件
CACHE MANIFEST # v0.11 首次下载后进行缓存的，一般会写版本号

CACHE:  # 需要被缓存的文件
js/app.js
css/style.css

NETWORK:  # 不需要被缓存的文件
resourse/logo.png

FALLBACK:
#表示如果访问第一个资源失败，那么就使用第二个资源来替换他，比如上面这个文件表示的就是如果访问根目录下任何一个资源失败了，那么就去访问offline.html。
/ /offline.html

var appCache = window.applicationCache;
switch (appCache.status) { 
    case appCache.UNCACHED: // UNCACHED == 0 
        return 'UNCACHED';
        break; 
    case appCache.IDLE: // IDLE == 1 
        return 'IDLE'; 
        break;
    case appCache.CHECKING: // CHECKING == 2
        return 'CHECKING'; 
        break;
    case appCache.DOWNLOADING: // DOWNLOADING == 3 
        return 'DOWNLOADING'; 
        break; 
    case appCache.UPDATEREADY: // UPDATEREADY == 4 
        return 'UPDATEREADY'; 
        break; 
    case appCache.OBSOLETE: // OBSOLETE == 5
        return 'OBSOLETE';break; 
    default:return 'UKNOWN CACHE STATUS';break;
};
```
