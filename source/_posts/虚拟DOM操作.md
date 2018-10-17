---
title: js技术
data: 2018/9/10 17:00
categories:
- Diary
tags:
- js 虚拟DOM
---
#### 怎样添加、移除、移动、复制、创建和查找节点？
创建新节点
> createDocumentFragment() //创建一个DOM片段
> createElement() //创建一个具体的元素
> createTextNode() //创建一个文本节点

```
//文档碎片    利于优化
var element  = document.getElementById('ul'); // assuming ul exists
var fragment = document.createDocumentFragment();
var browsers = ['Firefox', 'Chrome', 'Opera', 
    'Safari', 'Internet Explorer'];

browsers.forEach(function(browser) {
    var li = document.createElement('li');
    li.textContent = browser;
    fragment.appendChild(li);
});

element.appendChild(fragment);
```

添加、移除、替换、插入
> appendChild() //添加
removeChild() //移除
replaceChild() //替换
insertBefore() //插入

查找
>getElementsByTagName() //通过标签名称
getElementsByName() //通过元素的Name属性的值
getElementById() //通过元素Id，唯一性