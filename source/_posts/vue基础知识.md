---
title: Vue基础知识
date: 2018-09-05 14:00
tags: vue
categories: Diary
keywords: [vue]
---
#### vue.js的初引入
```
   <div id="app">
        {{message}}
        <span @click=handleClick();>切换</span>
    </div>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data(){
                return {
                    message:'hello Vue!',
                    x:0
                }
            },
            methods:{     
                handleClick(){
                    this.x++;
                    if(this.x % 2 == 0){
                        this.message='hello vue1';
                    }else{
                        this.message='hello vue2'; 
                    }
                }

            }
        })
    </script>
```

#### v-if v-else v-sho
> v-if操作的是DOM元素  
> v-show操作的是属性
> v-if： 判断是否加载，可以减轻服务器的压力，在需要时加载。
> v-show：调整css dispaly属性，可以使客户端操作更加流畅


#### watch与computed
>computed:计算属性将被混入到 Vue 实例中。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。
>注意如果你为一个计算属性使用了箭头函数，则 this 不会指向这个组件的实例，不过你仍然可以将其实例作为函数的第一个参数来访问。

>watch:尽量减少箭头函数使用（this指向不同），一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。

```
//computed:
    <div id="app">
        <input type="text" v-model="firstName" />
        <input type="text" v-model="lastName" /> 
        {{fullName}}
      </div>
  
      <script>
        new Vue({
          el: '#app',
          data: {
            firstName: 'hello',
            lastName: 'vue'
          },
          computed:{
            fullName:function(){
                return this.firstName+""+this.lastName;
            }
          }
        });

        var vm = new Vue({
            data: { a: 1 },
            computed: {
                // 仅读取
                aDouble: function () {
                return this.a * 2
                },
                // 读取和设置
                aPlus: {
                get: function () {
                    return this.a + 1
                },
                set: function (v) {
                    this.a = v - 1
                }
        }
  }
})
vm.aPlus   // => 2
vm.aPlus = 3
vm.a       // => 2  
vm.aDouble // => 4


//watch:
  <div id="app">
        <input type="text" v-model="firstName" />
        <input type="text" v-model="lastName" /> 
        {{fullName}}
      </div>
  
      <script>
        new Vue({
          el: '#app',
          data: {
            firstName: 'hello',
            lastName: 'vue',
            fullName: 'hello vue'
          },
            watch: {
            'firstName': function(newval, oldval) {
              console.log(newval,oldval);
              this.fullName = this.firstName + this.lastName;
            },
            'lastName': function(newval, oldval) {
              console.log(newval,oldval);
              this.fullName = this.firstName + this.lastName;
            }
          }
        });
      </script>   

    
      deep: true   深度watcher
      immediate: true 该回调将会在侦听开始之后被立即调用  
```

#### $mount  $watch
>$mount作用为手动挂载,可用于延时挂载

```
 app.$watch('temperature',function(newVal,oldVal){
     console.log(newVal,oldVal);
})

new Vue({
    data:{

    },
    ...
}).$mount('#app')
```




#### 数组排序(computed的具体使用)
```
<div id="app">
        {{itemSort}}        
    </div>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            created(){
                sortNumber=(a,b)=>{
                    return a-b
                }
            },
            data(){
                return {
                    items:[4,3,5,7,8,100,1,50,45,23],
                    
                }
            },
            methods:{  },
            computed:{
                itemSort:function(){
                    return this.items.sort(sortNumber);
                }, 
            }
        })
    </script>
```
#### 对象排序(computed的具体使用)
```
<div id="app">
        <ul>
            <li v-for='item in sortItem'>
                {{item.name}}-{{item.age}}
            </li>
        </ul>     
    </div>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            created(){
                  //数组对象方法排序:
                  sortByKey=(array,key)=>{
                            return array.sort(function(a,b){
                            var x=a[key];
                            var y=b[key];
                            return ((x<y)?-1:((x>y)?1:0));
                        });
                }
            },
            data(){
                return {
                    itemsArr:[
                        {name:'jili',age:22},
                        {name:'cheng',age:10},
                        {name:'lala',age:9}
                    ] 
                }
            },
            methods:{     
            },
            computed:{
                sortItem:function(){
                    return sortByKey(this.itemsArr,'age');
                }
            }
        })
    </script> 
```

#### v-text & v-html & v-model
```
//v-text可以简写为{{}},vue中有个指令叫做 v-once 可以通过v-once与v-text结合，实现仅执行一次性的插值
<span v-once>这个将不会随msg属性的改变而改变: {{ msg }}</span>
```

>v-html用于输出html，它与v-text区别在于v-text输出的是纯文本，浏览器不会对其再进行html解析，但v-html会将其当html标签解析后输出。

>需要注意的是：在生产环境中动态渲染HTML是非常危险的，因为容易导致XSS攻击。所以只能在可信的内容上使用v-html，永远不要在用户提交和可操作的网页上使用

>v-model通常用于表单组件的绑定，例如input，select等。它与v-text的区别在于它实现的表单组件的双向绑定，如果用于表单控件以外标签是没有用的。

```
 <div id="app">
        <p>原始文本信息：{{message}}</p>
        <h3>文本框</h3>
        <p>v-model:<input type="text" v-model="message"></p>
    </div>
    <script>
        var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        }
    })
    </script>
```

#### vue语法修饰符
+ .lazy：取代 imput 监听 change 事件。
+ .number：输入字符串转为数字。
+ .trim：输入去掉首尾空格。


#### 多选按钮与单选按钮
```
<!-- 多选按钮 -->
 <div id="app">
        <h3>多选绑定一个数组</h3>
       <p>
            <input type="checkbox" id="JSPang" value="JSPang" v-model="web_Names">
            <label for="JSPang">JSPang</label><br/>
            <input type="checkbox" id="Panda" value="Panda" v-model="web_Names">
            <label for="JSPang">Panda</label><br/>
            <input type="checkbox" id="PanPan" value="PanPan" v-model="web_Names">
            <label for="JSPang">PanPan</label>
            <p>{{web_Names}}</p>
       </p>
   </div>
    <script>
        var app=new Vue({
        el:'#app',
        data:{
            web_Names:[]
        }
    })
    </script>

    <!-- 单选按钮 -->
     <div id="app">
        <h3>单选按钮绑定</h3>
    <input type="radio" id="one" value="男" v-model="sex">
    <label for="one">男</label>
    <input type="radio" id="two" value="女" v-model="sex">
    <label for="one">女</label>
    <p>{{sex}}</p>
   </div>
    <script>
        var app=new Vue({
        el:'#app',
        data:{
            sex:'男'
        }
    })
    </script>
```


#### v-bind 指令
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
1、直接绑定class样式
```
<div :class="className">1、绑定classA</div>
```
2、绑定classA并进行判断，在isOK为true时显示样式，在isOk为false时不显示样式。
```
<div :class="{classA:isOk}">2、绑定class中的判断</div>
```
3、绑定class中的数组
```
<div :class="[classA,classB]">3、绑定class中的数组</div>
```
4、绑定class中使用三元表达式判断
```
<div :class="isOk?classA:classB">4、绑定class中的三元表达式判断</div>
```
5、绑定style
```
<div :style="{color:red,fontSize:font}">5、绑定style</div>
```
6、用对象绑定style样式
```
<div :style="styleObject">6、用对象绑定style样式</div>
var app=new Vue({
   el:'#app',
   data:{
       styleObject:{
           fontSize:'24px',
           color:'green'
            }
        }
})
```

#### 其他内部指令(v-pre & v-cloak)
> 在模板中跳过vue的编译，直接输出原始值。就是在标签中加入v-pre就不会输出vue中的data值了。
> <div v-pre>{{message}}</div>
> 这时并不会输出我们的message值，而是直接在网页中显示{{message}}


使用 v-cloak 防止页面加载时出现 vuejs 的变量名
```
<!-- 直接在css中添加 -->
[v-cloak] {
  display: none;
}
```



