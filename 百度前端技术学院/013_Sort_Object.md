### 对象

```
    var tree = {
        "id": 0,
        "name": "root",
        "left": {
            "id": 1,
            "name": "Simon",
            "left": {
                "id": 3,
                "name": "Carl",
                "left": {
                    "id": 7,
                    "name": "Lee",
                    "left": {
                        "id": 11,
                        "name": "Fate"
                    }
                },
                "right": {
                    "id": 8,
                    "name": "Annie",
                    "left": {
                        "id": 12,
                        "name": "Saber"
                    }
                }
            },
            "right": {
                "id": 4,
                "name": "Tony",
                "left": {
                    "id": 9,
                    "name": "Candy"
                }
            }
        },
        "right": {
            "id": 2,
            "name": "right",
            "left": {
                "id": 5,
                "name": "Carl",
            },
            "right": {
                "id": 6,
                "name": "Carl",
                "right": {
                    "id": 10,
                    "name": "Kai"
                }
            }
        }
    };

    // 假设id和name均不会重复，根据输入name找到对应的id
    function findIdByName(name) {
        for(var key in tree){
            if(tree["name"] === name){
                return tree["id"];
            }
            for(var ke in tree[key]){
                if(tree[key]["name"] === name){
                    return tree[key]["id"];
                }
                for(var k in tree[key][ke]){
                    if(tree[key][ke]["name"] === name){
                        return tree[key][ke]["id"];
                    }
                    for(var j in tree[key][ke][k]){
                        if(tree[key][ke][k]["name"] === name){
                            return tree[key][ke][k]["id"];
                        }
                        for(var l in tree[key][ke][k][j]){
                            if(tree[key][ke][k][j]["name"] === name){
                                return tree[key][ke][k][j]["id"];
                            }
                        }
                    }
                }
            }
        }
        return null;
    }

    // 假设id和name均不会重复，根据输入id找到对应的name
    function findNameById(id) {
        for(var key in tree){
            if(tree.id == id){
                return tree.name;
            }
            for(var i in tree[key]){
                if(tree[key].id == id){
                    return tree[key].name;
                }
                for(var j in tree[key][i]){
                    if(tree[key][i].id == id){
                        return tree[key][i].name;
                    }
                    for(var k in tree[key][i][j]){
                        if(tree[key][i][j].id == id){
                            return tree[key][i][j].name;
                        }
                        for(var l in tree[key][i][j][k]){
                            if(tree[key][i][j][k].id == id){
                                return tree[key][i][j][k].name;
                            }
                        }
                    }
                }
            }
        }
        return null;
    }

    // 把这个对象中所有的名字以“前序遍历”的方式全部输出到console中
    function getListWithDLR() {
        var result = [];
        for(var key in tree){
            if(key==="name"){
                result.push(tree["name"]);
            }
            for(var i in tree[key]){
                if(i==="name"){
                    result.push(tree[key]["name"]);
                }
                for(var j in tree[key][i]){
                    if(j==="name"){
                        result.push(tree[key][i]["name"]);
                    }
                    for(var k in tree[key][i][j]){
                        if(k==="name"){
                            result.push(tree[key][i][j]["name"]);
                        }
                        for(var l in tree[key][i][j][k]){
                            if(l==="name"){
                                result.push(tree[key][i][j][k]["name"]);
                            }
                        }
                    }
                }
            }
        }
        return result;
    }

    // 把这个对象中所有的名字以“中序遍历”的方式全部输出到console中
    function getListWithLDR() {

    }

    // 把这个对象中所有的名字以“后序遍历”的方式全部输出到console中
    function getListWithLRD() {

    }
```

### 排序

```
var arr1 = [43, 54, 4, -4, 84, 100, 58, 27, 140];
    console.log("arr1：" + arr.sort(function (a, b) {
            return a - b;
        }));

    var arr2 = ['apple', 'dog', 'cat', 'car', 'zoo', 'orange', 'airplane'];
    console.log("arr2：" + arr2.sort());

    var arr3 = [[10, 14], [16, 60], [7, 44], [26, 35], [22, 63]];
    console.log("arr3：" + arr3.sort(function (a, b) {
            return b.sort((i, j) = > (i - j)
            )
            [1] - a.sort((i, j) = > (i - j)
            )
            [1];
        }));

    var arr4 = [
        {
            id: 1,
            name: 'candy',
            value: 40
        }, {
            id: 2,
            name: 'Simon',
            value: 50
        }, {
            id: 3,
            name: 'Tony',
            value: 45
        }, {
            id: 4,
            name: 'Annie',
            value: 60
        }
    ];
    console.log(arr4.sort(function (a, b) {
        return a.value - b.value;
    }));

    var scoreObject = {
        "Tony": {
            "Math": 95,
            "English": 79,
            "Music": 68
        },
        "Simon": {
            "Math": 100,
            "English": 95,
            "Music": 98
        },
        "Annie": {
            "Math": 54,
            "English": 65,
            "Music": 88
        }
    };
    function getArray(obj) {
        var arr = [];
        for (var key in obj) {
            arr.push([key]);
            for (var i in obj[key]) {
                arr[arr.length - 1].push(obj[key][i]);
            }
        }
        return arr;
    }
    console.log("scoreObject：" + getArray(scoreObject));

    var menuArr = [
        [1, "Area1", -1],
        [2, "Area2", -1],
        [3, "Area1-1", 1],
        [4, "Area1-2", 1],
        [5, "Area2-1", 2],
        [6, "Area2-2", 2],
        [7, "Area1-2-3", 4],
        [8, "Area2-2-1", 6]
    ];
    function getObj(arr) {
        var obj = {};
        obj[arr[0][0]] = {};
        obj[arr[0][0]].name = arr[0][1];
        obj[arr[0][0]].subMenu = {};
        obj[arr[0][0]].subMenu[arr[2][0]] = {};
        obj[arr[0][0]].subMenu[arr[2][0]].name = arr[2][1];
        obj[arr[0][0]].subMenu[arr[3][0]] = {};
        obj[arr[0][0]].subMenu[arr[3][0]].name = arr[3][1];
        obj[arr[0][0]].subMenu[arr[3][0]].subMenu = {};
        obj[arr[0][0]].subMenu[arr[3][0]].subMenu[arr[6][0]] = {};
        obj[arr[0][0]].subMenu[arr[3][0]].subMenu[arr[6][0]].name = arr[6][1];
        
        obj[arr[1][0]] = {};
        obj[arr[1][0]].name = arr[1][1];
        obj[arr[1][0]].subMenu = {};
        obj[arr[1][0]].subMenu[arr[4][0]] = {};
        obj[arr[1][0]].subMenu[arr[4][0]].name = arr[4][1];
        obj[arr[1][0]].subMenu[arr[5][0]]= {};
        obj[arr[1][0]].subMenu[arr[5][0]].name = arr[5][1];
        obj[arr[1][0]].subMenu[arr[5][0]].subMenu = {};
        obj[arr[1][0]].subMenu[arr[5][0]].subMenu[arr[7][0]] = {};
        obj[arr[1][0]].subMenu[arr[5][0]].subMenu[arr[7][0]].name = arr[7][1];
        return obj;
    }
```


### 参考答案

[对象操作](https://github.com/yuyezhizhi/BaiduIfeStudy/blob/master/day22-24/day22-24%E5%AF%B9%E8%B1%A1%E6%93%8D%E4%BD%9C.html)

```
var tree = {
                "id": 0,
                "name": "root",
                "left": {
                    "id": 1,
                    "name": "Simon",
                    "left": {
                        "id": 3,
                        "name": "Carl",
                        "left": {
                            "id": 7,
                            "name": "Lee",
                            "left": {
                                "id": 11,
                                "name": "Fate"
                            }
                        },
                        "right": {
                            "id": 8,
                            "name": "Annie",
                            "left": {
                                "id": 12,
                                "name": "Saber"
                            }
                        }
                    },
                    "right": {
                        "id": 4,
                        "name": "Tony",
                        "left": {
                            "id": 9,
                            "name": "Candy"
                        }
                    }
                },
                "right": {
                    "id": 2,
                    "name": "right",
                    "left": {
                        "id": 5,
                        "name": "Carl",
                    },
                    "right": {
                        "id": 6,
                        "name": "Care",
                        "right": {
                            "id": 10,
                            "name": "Kai"
                        }        
                    }
                }
            }
            // 假设id和name均不会重复，根据输入name找到对应的id
            function findIdByName(name) {
                var id;
                // 遍历对象的方法
                function objFn(obj) {
                    for (var key in obj) {
                        // 如果对象中属性的值不是"object",那就看该对象的name属性值是否为输入的值，
                        if (typeof obj[key] != "object"){
                            if(obj["name"] == name) {
                                // 如果对象的name属性值符合输入的值，那么就把当前对象的id值赋值给外部声明的变量id
                                id = obj["id"];
                            }
                        }else {
                            // 如果对象中属性的值还是一个对象，那就重新遍历。
                            objFn(obj[key]);
                        }
                    }
                }
                // 执行方法
                objFn(tree);
                return id;
            }   
            // 假设id和name均不会重复，根据输入id找到对应的name
            function findNameById(id) {
                var name;
                function objFn(obj) {
                    for (var key in obj) {
                        if (typeof obj[key] != "object") {
                            if(obj["id"] == id) {
                                name = obj["name"];
                            }
                        }else {
                            objFn(obj[key]);
                        }
                    }
                }
                objFn(tree);
                return name;
            }
            // 把这个对象中所有的名字以“前序遍历”的方式全部输出到console中
            function getListWithDLR() {
                // 前序遍历定义：1.访问根节点。2.前序遍历左子树。3.前序遍历右子树。
                function objFn(obj) {
                    for (var key in obj) {
                        key == "name" && console.log(obj[key])
                        || key == "left" && objFn(obj[key])
                        || key == "right" && objFn(obj[key])
                    }
                }
                objFn(tree);
            }
            // 把这个对象中所有的名字以“中序遍历”的方式全部输出到console中
            function getListWithLDR() {
                // 中序遍历定义：1.中序遍历左子结点。2.访问根节点。3.中序遍历右子节点。
                function objFn(obj) {
                    for (var key in obj) {
                        key == "left" && objFn(obj[key]) 
                        || key == "name" && console.log(obj[key])
                        || key == "right" && objFn(obj[key])
                    }
                }
                objFn(tree);
            }
            // 把这个对象中所有的名字以“后序遍历”的方式全部输出到console中
            function getListWithLRD() {
                // 后序遍历定义：1.后序遍历左子结点。2.后续遍历右子节点。3.访问根节点。
                function objFn(obj) {
                    for (const key in obj) {
                        key == "left" && objFn(obj[key]) 
                        || key == "right" && objFn(obj[key])
                        || key == "name" && console.log(obj[key]+"-"+obj["id"])
                    }
                }
                objFn(tree);
            }
```


```
// 对象转为数组
            var scoreObject = {
                "Tony": {
                    "Math": 95,
                    "English": 79,
                    "Music": 68
                }, 
                "Simon": {
                    "Math": 100,
                    "English": 95,
                    "Music": 98
                }, 
                "Annie": {
                    "Math": 54,
                    "English": 65,
                    "Music": 88
                }
            }
            // 声明一个空数组
            var scoreArray = [];
            // 遍历对象属性，用属性，属性值中的"Math","English","Music"属性值
            for (const i in scoreObject) {
                const arr = [i, scoreObject[i]["Math"], scoreObject[i]["English"], scoreObject[i]["Music"]];
                scoreArray.push(arr);
            }
            console.log(scoreArray);
            
            // 数组转为对象：
            var menuArr = [
                [1, "Area1", -1],
                [2, "Area2", -1],
                [3, "Area1-1", 1],
                [4, "Area1-2", 1],
                [5, "Area2-1", 2],
                [6, "Area2-2", 2],
                [7, "Area1-2-3", 4],
                [8, "Area2-2-1", 6],
            ];
            // 利用数组每个子数组最后的编号对应于最初的编号，判断是否需要新建对象。
            function arrTurnObj(softNum = -1) {
                let newObj = {};
                for(let i in menuArr){
                    if(menuArr[i][2] == softNum){
                        newObj[menuArr[i][0]] = {
                            "name" : menuArr[i][1],
                            "subMenu" : arrTurnObj(menuArr[i][0])
                        }
                    }
                }
                return newObj;
            }
            console.log(arrTurnObj());
```
