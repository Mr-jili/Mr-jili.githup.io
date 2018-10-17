---
title: TypeScript技术胖读后感
date: 2018-09-04 9:40
tags: TypeScript
categories: Diary
keywords: [TypeScript,deno]
---
## deno的简读
>deno是使用Go语言代替C++重新编写跨平台底层内核驱动，上层仍然使用V8引擎，最终提供一个安全的TypeScript运行时
链接：https://github.com/denoland/deno



## TypeScript是什么？
>TypeScript 是一种由微软开发的自由和开源的编程语言。它是 JavaScript 的一个超集，TypeScript 在 JavaScript 的基础上添加了可选的静态类型和基于类的面向对象编程。

## TypeScript和JavaScript的对比
>TypeScript是一个应用程序级的JavaScript开发语言。（这也表示TypeScript比较牛逼，可以开发大型应用，或者说更适合开发大型应用）
>TypeScript是JavaScript的超集，可以编译成纯JavaScript。这个和我们CSS离的Less或者Sass是很像的，我们用更好的代码编写方式来进行编写，最后还是有好生成原生的JavaScript语言。
>TypeScript跨浏览器、跨操作系统、跨主机、且开源。由于最后他编译成了JavaScript所以只要能运行JS的地方，都可以运行我们写的程序，设置在node.js里。
>TypeScript始于JavaScript，终于JavaScript。遵循JavaScript的语法和语义，所以对于我们前端从业者来说，学习前来得心应手，并没有太大的难度。
>TypeScript可以重用JavaScript代码，调用流行的JavaScript库。
>TypeScript提供了类、模块和接口，更易于构建组件和维护。

## TypeScript使用流程
>首先安装TypeScript
```
npm install typescript -g
tsc --version
```
编写HelloWorld程序
>终端输入：
1.npm init -y (初始化项目，生成package.json文件)
2.tsc --init (它是一个TypeScript项目的配置文件，可以通过读取它来设置TypeScript编译器的编译参数)
3.npm install @types/node --dev-save  (主要是解决模块的声明文件问题)
4.编写hello.ts文件
```
var a:string = "HelloWorld"
console.log(a)
```
>5.tsc hello.ts  编译成hello.js文件
>6.node hello.js

## TypeScript中的数据类型有
>Undefined
>Number
>String
>Boolean
>enum 枚举类型
>any 任意类型
>void 空类型
>Array
>Tuple 元祖类型
>Null

>Number类型有
+ NaN
+ Infinity :正无穷大。
+ -Infinity：负无穷大。


enum类型
>一般应用于固定数据
```
// enum REN{ nan , nv ,yao}
// console.log(REN.yao)  //返回了2，这是索引index，跟数组很象。

enum REN{
    nan = '男',
    nv = '女',
    yao= '妖'
}
console.log(REN.yao)  //返回了妖 这个字

```

any类型
>TypeScript友好的为我们提供了一种特殊的类型any，比如我们在程序中不断变化着类型，又不想让程序报错，这时候就可以使用any了。
```
var t:any =10 
t = "jspang"
t = true
console.log(t)
```

<div style="color:red;">Tuple类型(元祖类型)</div>
>元祖是一种特殊的数组，元祖类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同
```
//声明一个元祖类型
let x : [string,number]
//正确的初始化
x = ['hello',10]
//错误的初始化方法
x = [10,'hello']
```



## 函数中传参
>举个typescript语法的例子：
```
function searchXiaoJieJie3(...xuqiu:string[]):string{
    let  yy:string = '找到了'
    for (let i =0;i<xuqiu.length;i++){
        yy = yy + xuqiu[i]
        if(i<xuqiu.length){
            yy=yy+'、'
        }
    }
    yy=yy+'的小姐姐'
    return yy
}
var result:string  =  searchXiaoJieJie3('22岁','大长腿','瓜子脸','水蛇腰')
console.log(result)
```

局部变量·全局变量·var与let和javascript差不多，不一一言论

## 引用类型-数组
声明数组的方法
>由let var 关键字来实现，ts中声明较复杂
```
let arr1:number[ ]     //声明一个数值类型的数组
let arr2:Array<string>  //声明一个字符串类型的数组
```
数组赋值
+ 字面量赋值法：直接使用“[ ]”对数组进行赋值。
```
//定义一个空数组，数组容量为0
let arr1:number[] = [] 
//定义一个数组时，直接给数组赋值
let arr2:number[] = [1,2,3,4,5]
//定义数组 的同事给数组赋值
let arr3:Array<string> = ['jspang','技术胖','金三胖']
let arr4:Array<boolean> = [ true,false,false]

//切记：
let arr5:number[] = [1,2,true]  //报错 必须存储number类型的数据
```
+ 构造函数赋值法：
```
let arr1:number[] = new Array()
let ara2:number[] = new Array(1,2,3,4,5)
let arr3:Array<string> = new Array('jspang','技术胖','金三胖')
let arr4:Array<boolean> = new Array(true,false,false)
```
## 引用类型-字符串
+ 基本类型字符串：由单引号或者双引号括起来的一串字符串。
+ 引用类型字符串：用new 实例化的 String类型。
```
let jspang:string = '技术胖'
let jspanga:String = new String("jspang.com")
console.log(jspang)  //技术胖
console.log(jspanga) //[String: 'jspang.com']
```

#### replace替换
```
let something:string = "清早起来打开窗，心情美美的，我要出去找小姐姐，心情美美的。"
let xiaoJieJie:string = "小姐姐"
console.log(something.replace(xiaoJieJie,'小哥哥'))  // /小姐姐/g全局匹配
```


## 引用类型-日期对象


1.不传递任何参数

```
let d:Date = new Date()
console.log(d)  //2018-09-06T06:48:12.504Z
```
2.传递一个整数
```
let d:Date = new Date(1000)
let da:Date = new Date(2000)
console.log(d)  //1970-01-01T00:00:01.000Z
console.log(da) //1970-01-01T00:00:02.000Z
```

3.传递一个字符串
```
let d1:Date = new Date('2018/09/06 05:30:00')
let d2:Date = new Date('2018-09-06 05:30:00')
let d3:Date = new Date('2018-09-06T05:30:00')
console.log(d1)  
console.log(d2)
console.log(d3)  //2018-09-05T21:30:00.000Z结果一样
```

4.传递表示年月日时分秒的变量
>let d:Date = new Date(year,month,day,hours,minutes,seconds,ms);

+ year 表示年份，4位数字。
+ month表示月份，数值是0(1月)~11(12月)之间的整数。
+ day 表示日期。数值是1~31之间的整数。
+ hours 表示小时，数值是0-23之间的整数。
+ minutes 表示分钟数，数值是0~59之间的整数。
+ seconds 表示秒数，数值是0~59之间的整数。
+ ms 表示毫秒数，数值是0~999之间的整数。

## 引用类型-正则表达式
#### 构造函数法
>构造函数中可以传一个参数，也可以传递两个参数。一个是字符串描述，另一个是修饰符，比如g是全局修饰符，i是忽略大小写，m是多行模式。

```
let reg1:RegExp = new RegExp("jspang")  //表示字符串规则里含有jspang
console.log(reg1)
let reg2:RegExp = new RegExp("jspang",'gi')
console.log(reg2)
```

#### 字面量法
```
let reg3:RegExp = /jspang/
let reg4:RegExp = /jspang/gi
```
#### RegExp中的常用方法
>RegExp对象包含两个方法：test( )和exec( ),功能基本相似，用于测试字符串匹配。
+ test(string) ：匹配。在字符串中查找是否存在指定的正则表达式并返回布尔值，如果存在则返回 true，不存在则返回 false。
+ exec(string) : 捕获。用于在字符串中查找指定正则表达式，如果 exec() 方法执行成功，则返回包含该查找字符串的相关信息数组。如果执行失败，则返回 null。
