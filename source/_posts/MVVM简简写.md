---
title: MVVM双向数据绑定源码（简单理解）
data: 2018/7/31 14:00
categories:
- Diary
tags:
- vue
- MVVM
---
Vue.js 是采用 Object.defineProperty 的 getter 和 setter，并结合观察者模式来实现数据绑定的。当把一个普通 Javascript 对象传给 Vue 实例来作为它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化。
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>双向数据绑定</title>
</head>
<body>
    <input type="text" id="message" />
    <div id="msg"></div>
    <script>
        var obj = {};
        Object.defineProperty(obj, "data", {
            get: function () {
                console.log("get")
            },
            set: function (newValue) {
                document.getElementById("message").value = newValue
                document.getElementById("msg").innerText = newValue
            } 
        })
        document.getElementById("message").onkeyup=function (e) {
            console.log(e.target.value);
            obj.data = e.target.value;
        };
        
//柯里化思想
//         var curry = function(func){
//     var args = [].slice.call(arguments,1);
//     console.log(args);
//     return function(){
//         var newArgs = args.concat([].slice.call(arguments));
//         console.log(newArgs);  
//         return func.apply(this,newArgs);
//     }
// }
// function add(a, b) {
//     return a + b;
// }

// var addCurry = curry(add,1);
// console.log(addCurry(3));//3
    </script>
</body>
</html>
```
这里只是简单的了解下，待续~~~ 
详细了解 ：https://github.com/Mr-jili/mvvm  





