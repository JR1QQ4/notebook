# vue

1.v-cloak v-text v-html ，添加文本

- v-clock：解决插值表达式闪烁的问题，替换文本闪烁
- v-text：会覆盖元素中原本的内容
- v-html：会把data中的标签当成成HTML显示

```
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
    <div id="app">
        <p v-cloak>{{ msg }}</p>
        <p v-text='msg'></p>
        <div v-html='msg2'></div>
    </div>
    <script>
            var vue = new Vue({
                el: '#app',  // 指定要控制的区域
                data: {
                    msg: 'Hello World!',
                    msg2: '<h1>Hello world!</h1>'
                },  // 指定控制的区域内要用到的数据
                methods: {}  // 自定义方法的对象
            })
    </script>
```

2.v-bind：用于属性的绑定，简写是`:`

```
<input type="button" value="按钮" v-bind:title="mytitle">
<input type="button" value="按钮" :title="mytitle">
<input type="button" value="按钮" v-bind:title="mytitle+123">
var vue = new Vue({
    el: '#app',
    data: {
        mytitle: '我是按钮'
    }
})
```

3.v-on：用于绑定事件，简写是`@`

```
<input type="button" value="按钮" @click="getNow">
<input type="button" value="按钮" v-on:click="getNow">
var vue = new Vue({
    el: '#app',
    methods: {
        getNow: function () {
            alert(Date.now());
        }
    }
})
```

4.方法，this:绑定事件`@`，`methods`中访问`data`使用`this`，箭头函数中的`this`就是`data`中的`this`，也可以先定义`var _self = this`，然后在定时器中使用`_self`

```
    <div id="app">
        <input type="button" @click="loop" value="循环"></input>
        <input type="button" @click="stop" value="暂停"></input>
        <p>{{ msg }}</p>
    </div>
    <script>
        var vue = new Vue({
            el: '#app',
            data: {
                msg: "我是跑马灯~~~~！",
                timerId: null
            },
            methods: {
                loop: function () {
                    if (this.timerId != null) {
                        return;
                    }
                    this.timerId = setInterval(() => {
                        var start = this.msg.substring(0,1);
                        var end = this.msg.substring(1);
                        this.msg = end + start;
                    }, 100);
                },
                stop: function () {
                    clearInterval(this.timerId);
                    this.timerId = null;
                }
            }
        });
    </script>
```

5.事件修饰符：

-  .stop：阻止事件冒泡
-  .prevent：阻止默认行为
-  capture：设置成捕获阶段触发
-  .self：只有当前元素才会触发，只能阻止自己的冒泡行为
-  .once：事件只触发一次，添加的prevent也只触发一次

```
    <div id="app">
        <div id="outer" @click="outerClick">
            <input type="button" value="点击事件" @click.stop="btnClick">
        </div>
    </div>
    <a href="http://www.baidu.com" @click.prevent>百度</a>
    <div id="outer" @click.capture="outerClick">
```

6.v-model 和双向数据绑定，`只能用于表单元素中`，v-bind 只能实现单向数据绑定

```
    <div id="app">
        <h4>{{ msg }}</h4>
        <input type="text" v-bind:value="msg"> 
        <input type="text" v-model="msg">
    </div>   
```

7.使用样式

（1）使用class样式：

-  数组：`<h1 :class="['letter', 'italic']">Lorem ipsum dolor</h1>`
    +  数组中使用三元表达式：`<h1 :class="['letter', 2>1?'active':'']">Lore</h1>`
    +  数组中使用对象：`<h1 :class="['letter',{'active':flag}]">Loremolor</h1>`
    +  直接使用对象：`<h1 :class="{color:true,active:true}">Lorem ipsum</h1>`
        *  注意：属性引号可有可无，属性值是一个标识符，flag是data中定义的
        *  `<h1 :class="obj">Lorem</h1> data: {obj:{color:true,active:true}}`

（2）使用style内联设置样式：

- 内联：`<h3 :style="{width:'300px',color:'pink'}">Lorem, ipsum.</h3>`
- 在data中定义：`<h3 :style="obj">Lorem</h3> obj: {'font-size':'30px'}` 
- 使用数组形式：`<h3 :style="[styleobj,styleobj2]">Lorem</h3>`


8.v-for 循环：

- 普通数组：`v-for="(item,i) in list"` item是数组中的每个值
- 对象数组：`v-for="(item,i) in list2"` item是数组中的每个对象
- 对象：`v-for="(value,key,i) in list3"`

```
data: {
    list: [1, 2, 3, 4, 5, 6],
    list2: [{ id:1,name: "zs1" },{ id:2,name: "zs2" },{ id:3,name: "zs3" },],
    list3: {id:1,name:'张三',age:'23'}
}
<div v-for="i in 10">{{i}}</div>
<div v-for="(item,i) in list">index：{{i}}--value：{{ item }}</div>
<div v-for="item in list2">id:{{item.id}}--name:{{item.name}}</div>
<div v-for="(item,i) in list2">id:{{item.id}}--name:{{item.name}}--index：{{i}}</div>
<div v-for="(value,key,i) in list3">{{value}}--{{key}}--{{i}}</div>
```

- 为了每一项的唯一性，需要添加一个key，key只能使用number和string类型，并用v-bind绑定

```
<div v-for="(item,i) in list2" :key="item.id" class="dv">
    <input type="checkbox">{{item}}----{{i}}
</div>
```

9.v-if 与 v-show：

-  v-if：根据条件判断删除和创建元素
-  v-show：根据条件显示和隐藏元素，`display`

```
const vue = new Vue({ el: '#app',data: { flag: true} });
<div id="app">
    <input type="button" value="toggle" @click="flag=!flag">
    <div v-if="flag">11111</div>
    <div v-show="flag">222222</div>
</div>
```

10.v-for遍历函数返回值：

```
<tr v-for="item in search(keywords)" :key="item.id">
    <td>{{item.id}}</td>
    <td>{{item.name}}</td>
    <td>{{item.ctime}}</td>
    <td><button type="button" class="btn btn-link" @click="del(item.id)">删除</button></td>
</tr>
search(keywords){
    return this.list.filter(ele => {
        if(ele.name.includes(keywords)){
            return true;
        }
    });
}
```

11.过滤器，可以在两个地方使用：`mustache`插值和`v-bind`表达式：

（1）全局过滤器

```
过滤器调用时的格式： <p>{{ name | nameope(data) }}</p>
过滤器语法，放在vue实例之前：Vue.filter('nameope',function(naem,data){ ... })

过滤器函数形参的第一个值永远都是name管道前面的值，后面的值是传入的值。
过滤器可以多次过滤：<p>{{ name | nameope | test }}</p>
```
 
（2）私有过滤器，定义在实例内部`filters`里面，私有过滤器优先于全局过滤器

```
    const vue = new Vue({
            el: '#app',
            data: {},
            filters:{
                dataFormat:function(data){}
            }
        });
```

12.自定义键值，内置了一些按键码：enter、tab、delete、esc、space、up、down、left、right

```
<input type="text" class="form-control" v-model="name" @keyup.enter="add">
<input v-on:keyup.13="submit">
Vue.config.keyCodes = {f2:113,"media-play-pause": 179}
<input type="text" @keyup.media-play-pause="method">
```

13.自定义指令，定义时指令名称不需要加`v-`，插入到元素中时需要加`v-`：

```
<input type="text" v-focus>
Vue.directive('focus', {
    inserted: function (el) { // 被绑定元素插入父节点时调用 
        el.focus(); // el:指令所绑定的元素，可以用来直接操作 DOM ，固定第一个参数 
    },
    bind: function(el){},  // 只调用一次，第一次绑定到元素时调用，此时没插到DOM树中
    update: function(el, binding, vnode){}  // 所在组件的 VNode 更新时调用
})

directives: {  // 局部自定义组件使用复数，directives
  focus: {  inserted: function (el) {  el.focus() } }
}

<div v-color="'orange'">123</div>  // 传入字符串需要有单双引号
Vue.directive('color', {  // bind 和 update 的简写
    bind: function (el, binding) {
        el.style.backgroundColor = binding.value
    }
})
```

14.生命周期：从实例创建运行到销毁，执行的一系列事件。

-  创建时的函数：beforeCreate、created、beforeMount、mounted
-  运行时的函数：beforeUpdate、updated
-  销毁时的函数：beforeDestroy、destroyed

```
<div id="app">
    <input type="button" @click="msg='new message!'" value="修改数据">
    <h1 id="h1">{{ msg }}</h1>
</div>
const vue = new Vue({
    el: '#app',
    data: {    msg: "我是数据"},
    methods: {    show: function () {    console.log(this.msg);}},
    beforeCreate(){    console.log(this.msg);   },
    created(){    console.log(this.msg);    this.show();},
    beforeMount(){    console.log(document.getElementById("h1").innerText);},
    mounted(){   console.log(document.getElementById("h1").innerText);},
    beforeUpdate(){
        console.log(document.getElementById("h1").innerText);
        console.log("beforeUpdate:"+this.msg);
    },
    updated(){
        console.log(document.getElementById("h1").innerText);
        console.log("updated:"+this.msg);
    },
    beforeDestroy(){    console.log("beforeDestroy:"+this.msg);},
    destroyed(){    console.log("destroyed:"+this.msg);}
});
```

15.vue-resource：实现异步加载需要使用到 vue-resource 库，Vue.js 2.0 版本推荐使用 axios 来完成 ajax 请求。

（1）vue-resource

```
Vue.http.options.emulateJSON = true;  // 全局配置
Vue.http.options.root = '/root';  // 配置了之后，get(url,...)中的url使用相对路径

get(url, [options])
jsonp(url, [options])
post(url, [body], [options])

this.$http.get('get.php',{params : {a:1,b:2}}).then(function(res){
    document.write(res.body);    
},function(res){
    console.log(res.status);
});

 this.$http.post('/try/ajax/demo_test_post.php',{name:"菜鸟教程",url:"http://www.runoob.com"},{emulateJSON:true}).then(function(res){
    document.write(res.body);    
},function(res){
    console.log(res.status);
});
```

16.过渡和动画

（1）过渡和动画：分成6个阶段：v-enter，v-enter-active，v-enter-to，v-leave，v-leave-active，v-leave-to

```
// 此时定义的是全局类，所有过渡都按照这个效果做
.v-enter-active,
.v-leave-active {  // 在过渡过程中生效
    transition: all 10s ease;
}
.v-enter,
.v-leave-to {  // 过渡生效时的状态
    opacity: 0;
    transform: translateX(200px);
}
.v-enter-to,
.v-leave {  // 离开过渡的结束状态
    opacity: 1;
} 

<div id="app">
    <input type="button" value="toggle" @click="show=!show">
    <transtion>  
        <p v-if="show">Lorem ipsum dolor sit amet.</p>
    </transtion>
</div>

<transtion name="my">  // 自定义类前缀，定义之后，类名变成 .my-enter,.my-leave-to
    <p v-if="show">Lorem ipsum dolor sit amet.</p>
</transtion>
```

（2）动画 JavaScript 钩子，钩子函数第一个参数el，表示执行动画的那个元素，是个原生的DOM对象。
在 enter 和 leave 中必须使用 done 进行回调，enter 中的 done() 相当于调用 afterEnter。

```
// 函数相当于动画的一个执行过程
<transition
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"

  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>

methods: {
  beforeEnter: function (el) {},
  // 当与 CSS 结合使用时,回调函数 done 是可选的
  enter: function (el, done) {
    el.offsetWidth;   // 这里需要添加一个offset系列属性，不然没有过渡，offsetHeight,offsetLeft,offsetTop
    ...
    done()
  },
  afterEnter: function (el) {},
  enterCancelled: function (el) {},
  beforeLeave: function (el) {},
  // 当与 CSS 结合使用时，回调函数 done 是可选的
  leave: function (el, done) {
    done()
  },
  afterLeave: function (el) {},
  // leaveCancelled 只用于 v-show 中
  leaveCancelled: function (el) {}
}
```

（3）渲染动画

```
// 可以使下面项缓缓的移上来
.v-move {
    transition: all .5s ease;
}
.v-leave-active {
    position: absolute;
}

// 对于渲染的，需要使用transition-group，并且项中要有 :key 属性
<ul>
    <transition-group>
        <li v-for="(item,i) in list" @click="del(i)" :key="item.id">
            {{item.id}}------------{{item.name}}--------------
        </li>
    </transition-group>
</ul>
```

（4）初始渲染过渡

```
// 这个可以完成初始渲染过渡，但是查看元素，li 嵌套在 span 里
<ul>
    <transition-group appear>
        <li v-for="(item,i) in list"></li>
    </transition-group>
</ul>

// 把 li 渲染到 ul 中
<transition-group appear tag="ul">
    <li v-for="(item,i) in list"></li>
</transition-group>
```

17.组件，模块化是从代码逻辑的角度进行划分的，方便代码分层开发，保证每个功能模块的职能单一；组件化是从UI界面的角度进行划分的，方便UI组件的重用

（1）创建全局组件，如果组件名称使用驼峰命名法，使用的时候需要用小写并用`-`隔开

```
// 第一种方式，使用Vue.extend
<login></login>
var login = Vue.extend({
    template:"<h1>登录</h1>"
})
Vue.component("login",loginTemplate);

// 第二种方式，直接写入模板，模板中只能有一个root根节点
<register></register>
Vue.component("register",{
    template: "<h1>注册</h1>"
});

// 第三种方式，把模板放在 #app 外面定义
<div id='app'>
    <index></index>
</div>
<template id="login">
    <div>
        <h1>index template</h1>
    </div>
</template>
Vue.component("index",{
    template:"#login"
})
```

（2）创建私有组件

```
<div id='app'>
    <login></login>
</div>
<template id="com1">
    <div>
        <h1>私有组件</h1>
    </div>
</template>
const vue = new Vue({
    el: '#app',
    components:{
        login: {  template: "#com1";  }
    }
});
```

（3）组件中的data必须是一个方法，并且返回一个对象，使用方式和实例中的data一样

```
<div id='app'>
    <com1></com1>
    <com1></com1>
    <com1></com1>
</div>
<template id="tem1">
    <div>
        <input type="button" value="加一" @click="add">
        <h1>{{ count }}</h1>
    </div>
</template>
Vue.component("com1",{
    template:"#tem1",
    methods: {
        add(){
            this.count++;
        }
    },
    data: function(){
        return { count: 0 }
    }
});
```

（4）组件切换，component中`:is`的值是字符串，需要带引号，变量不需要引号

```
<div id='app'>
    <a href="#" @click="componentId='login'">登录</a>
    <a href="#" @click="componentId='register'">注册</a>
    <component :is="componentId"></component> 
</div>
Vue.component("login", {
    template: "<h3>登录组件</h3>"
})
Vue.component("register", {
    template: "<h3>注册组件</h3>"
})
const vue = new Vue({
    el: '#app',
    data: {
        componentId: "login"
    }
})
```

（5）组件切换时的过渡，mode解决进入和离开同时发生的问题

```
.v-enter,
.v-leave-to {
    opacity: 0;
}
.v-enter-active,
.v-leave-active {
    transition: all .5s;
}
<transition mode="out-in">
    <component :is="componentId"></component>
</transition>
```

（6）实例向组件中传值

-  默认组件中不能访问实例中的data；
-  实例中的data优先于组件中的data；
-  实例中的data需要在在调用组件的元素中，绑定一个自定义属性，属性值是实例中的data，然后在组件`props数组`中定义一下这个属性，就能在组件中使用实例中的data了
-  绑定除了`v-bind`绑定属性，还有其他绑定，`v-on`可以绑定事件

```
<div id='app'>
    <com1 v-bind:newMsg="msg"></com1>
</div>
const vue = new Vue({
    el: '#app',
    data: {
        msg: "我是实例中的信息"
    },
    methods: {},
    components: {
        com1: {
            data: function () {
                return {
                    msg: "我是组件中的信息"
                }
            },
            template: "<h1>我是组件----{{newmsg}}</h1>",
            props:['newmsg']  // 绑定中用驼峰，使用需要变成小写的
        }
    }
});
```

（7）组件向实例中传值

```
<div id='app'>
    <h1>Lorem ipsum dolor, sit amet consectetur adipisicing elit.</h1>
    <com1 v-on:func="show"></com1>  // func存放实例中方法的引用
</div>
<template id="tmp1">
    <div>  // 调用组件自己的方法clk
        <input type="button" @click="clk" value="组件中的按钮">
    </div>
</template>
const vue = new Vue({
    el: '#app',
    data: {
        dataFromComponent: null
    },
    methods: {
        show(data) {
            console.log("触发了父组件中的首位方法");
            console.log(data);
            this.dataFromComponent = data;  // 存储组件传来的值
        }
    },
    components: {
        com1: {
            template: "#tmp1",
            data: function () {
                return {msg: "template template"}
            },
            methods: {
                clk() {  // 用于触发实例中的方法
                    this.$emit('func',this.msg);  // 组件调用实例中的值
                }
            }
        }
    }
});
```

（8）ref获取DOM元素和组件引用，可以访问组件的元素，方法和data

```
<div id='app'>
    <h3 ref="myh3">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Error, eaque?</h3>
    <input type="button" value="按钮" ref="mybtn" @click="myElements">
    <login ref="lg"></login>
</div>
<template id="tmp1">
    <div>
        <h3>登录组件</h3>
    </div>
</template>
var login = {
    data: function () {
        return { msg: "123" }
    },
    methods: {
        show() {
            console.log("组件方法");
        }
    },
    template: "#tmp1"
};
const vue = new Vue({
    el: '#app',
    data: {},
    methods: {
        myElements() {
            this.$refs.reference.style.color = "orange";
            console.log(this);  // this.$refs.lg.show(); this.$refs.lg.msg;
        }
    },
    components: {
        login
    }
});
```

18.vue-router

（1）普通

```
// 引入 vue-router
    <script src='../vue.js'></script>
    <script src="../vue-router.js"></script>
// 设置
    var login = {
        template: "<h1>登录</h1>"
    }
    var register = {
        template: "<h1>注册</h1>"
    }

    const router = new VueRouter({
        routes: [
            { path: "/login", component: login },
            { path: "/register", component: register }
        ],
        linkActiveClass: "myactive"  // 设置router-link样式
    })
    const vue = new Vue({
        el: '#app',
        router: router
    });
// 使用
    <div id='app'>
        <!-- <router-link to="/login">Login</router-link>
        <router-link to="/register">Register</router-link> -->
        <a href="#/login">Login</a>
        <a href="#/register">Register</a>
        <router-view></router-view>
    </div>

// router-link 默认渲染成 a 标签，tag 选择渲染的标签
    <router-link to="/login" tag="span">Login</router-link> 
// 使用 router-link 渲染的标签会有一个类 class="router-link-exact-active router-link-active"
// 修改类样式处理直接使用类名修改，还能使用配置项 linkActiveClass 添加类名

// 重定向
{ path: "/", redirect: "/login" }
```

（2）传值

```
// 第一种传值
<router-link to="/login?id=123" tag="span">Login</router-link>
var login = {
    template: "<h1>登录---{{ $route.query.id }}</h1>",
    created() {
        console.log(this.$route)
    },
}
> {name: undefined, meta: {…}, path: "/login", hash: "", query: {…}, …}
> query: {id: "123"}

// 第二种传值
<router-link to="/register/name=zhangsan">Register</router-link>
var register = {
    template: "<h1>注册</h1>",
    created() {
        console.log(this.$route)
    },
}
{ path: "/register/:name", component: register }
> {name: undefined, meta: {…}, path: "/register/name=zhangsan", hash: "", query: {…}, …}
> params: {name: "name=zhangsan"}
```

（3）子路由

```
<template id="login">
    <div>
        <h1>登录</h1>
        <router-link to="/login/acount">Acount</router-link>
        <router-link to="/login/password">Password</router-link>
        <router-view></router-view>
    </div>
</template>

routes: [{
    path: "/login", 
    component: login, 
    children: [{ path: "acount", component: acount },
        { path: "password", component: password }]
}]
```

（4）视图name

```
<router-view></router-view>
<router-view name="main"></router-view>
<router-view name="footer"></router-view>

const router = new VueRouter({
    routes:[
        {path:"/",components:{
            "default":header,
            "main":main,
            "footer":footer
        }}
    ]
})
```

19.watch，可用于监听路由的改变

```
<div id='app'>
    <label for="">Firsetname:<input type="text" v-model="firstname"></label> 
    <label for="">Lastname:<input type="text" v-model="lastname"></label> 
    <label for="">Fullname:<input type="text" v-model="fullname"></label> 
</div>
const vue = new Vue({
    el: '#app',
    data: {
        firstname:"",
        lastname:"",
        fullname:""
    },
    methods: {},
    watch: {
        "firstname":function (newVal,oddVal) {            
            this.fullname = this.firstname + "-" + this.lastname
            console.log(newVal)
            console.log(oddVal)
        },
        "lastname":function(newVal,oddVal){
            this.fullname = this.firstname + "-" + this.lastname
        },
        "$route.path":function(newUrl,oldUrl){}
    }
});
```

20.computed，fullname会缓存，再次使用不会再触发函数，fullname 会因为fname和lanme因子改变而触发函数

```
<div id='app'>
    <label for=""><input type="text" v-model="fname"></label>
    <label for=""><input type="text" v-model="lname"></label>
    <label for=""><input type="text" v-model="fullname"></label>
    <h2>{{ fullname }}</h2>
    <h2>{{ fullname }}</h2>
    <h2>{{ fullname }}</h2>
</div>
const vue = new Vue({
    el: '#app',
    data: {
        fname:"",
        lname:""  // 这里没有定义 fullname
    },
    methods: {},
    computed: {
        "fullname":function(){
            return this.fname + "-" +this.lname
        }
    },
});
```
