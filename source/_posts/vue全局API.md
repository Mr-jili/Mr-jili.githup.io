---
title: Vue全局API
date: 2018-09-06 17:00
tags: vue
categories: Diary
keywords: [vue]
---
## Vue.directive 自定义指令
#### Vue.directive 自定义指令
代码说明:
```
<div id="app">
        <div v-jili="color" id="demo">
            {{num}}
        </div>
        <div>
             <button @click="add">Add</button>
        </div>
    </div>
    <script>
        Vue.directive('jili',function(el,binding,vnode){ 
            console.log(el,binding,vnode);   //el  当前元素    binding 包含指令的很多信息。
            el.style='color:'+binding.value;
        });
        var app=new Vue({
            el:'#app',
            data:{
                num:10,
                color:'green'
            },
            methods:{
                add:function(){
                    this.num++;
                }
            }
        })
    </script>
```

#### 自定义指令的生命周期
1.bind          被绑定
2.inserted      绑定到节点
3.update        组件更新
4.componentUpdated 组件更新完成
5.unbind       解绑


## Vue.extend构造器
>扩展实例构造器,意为当有多个地方使用同一个标签路径，我们在实例上封装一个自动调用的方法，方法，并挂载到自定义元素上

```
var authorExtend = Vue.extend({
    template:"<p><a :href='authorUrl'>{{authorName}}</a></p>",
    data:function(){
    return{
          authorName:'度娘',
          authorUrl:'http://www.baidu.com'
          }
    }
});

//new authorExtend().$mount('元素')
```

## Vue.set全局操作
>Vue.set 的作用就是在构造器外部操作构造器内部的数据、属性或者方法。

#### Vue.set存在意义
> 由于Javascript的限制，Vue不能自动检测以下变动的数组。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>Vue.set 全局操作</title>
</head>
<body>
    <h1>Vue.set 全局操作</h1>
    <hr>
    <div id="app">
        <ul>
            <li v-for=" aa in arr">{{aa}}</li>
        </ul>
    </div>
    <button onclick="add()">外部添加</button>
    <script type="text/javascript">
        function add(){
            console.log("我已经执行了");
           app.arr[1]='ddd';          //不能变动
           //Vue.set(app.arr,1,'ddd');
        }
        var outData={
            arr:['aaa','bbb','ccc']
        };
        var app=new Vue({
            el:'#app',
            data:outData
        })
    </script>
</body>
</html>
```