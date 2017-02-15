---
title: JavascriptDOM 编程艺术
date: 2016-11-03 11:01:27
tags: JavaScript
categories: JavaScript
---
***
## 重要的DOM Core方法
- getElementById
- getElementByTagName
- getAttribute
- setAttribute
- example.setAttribute("id","idName")

## DOM Core方法和HTML-Core方法区别

## childNodes属性
用于获取所有子元素
<!-- more -->
## nodeType属性
- 元素节点 nodeType值是1。
例如 div ,p
- 属性节点 nodeType值为2。
例如 title
- 文本节点 nodeType值为3。
例如 “hello world”

## nodeValue属性
- firstChild
获取的数组中的第一个元素
- lastChild
获取的数组中的最后一个元素

## 三个重要的函数
1. addLoadEvent方法
```
function addLoadEvent(func){
var oldonload = window.onload;
if(typeof window.onload != 'function'){
   window.onload = func;
  }else{
   window.onload = function(){
      oldonload();
      func();
     }
   }
}
```
if(typeof window.onload != ‘function’)的作用是判断window.onload事件有没有绑定函数。
2. insertAfter函数
```
function insertAter(newElement,targetElement){
   var parent = targetElement.parentNode;
   if(parent.lastChild == targetElement){
      parent.appendChild(newElement);
   }else{
      parent.insertBefore(newElement,targetElement.nextSibling);
   }
}
```
用于把新元素插入到一个元素之后
3. addClass函数
```
function addClass(element,value){
if(!element.className){
   elment.className = value;
  }else{
   newClassName = element.className;
   newClassName += " ";
   newClassName += value;
   element.className = newClassName;
  }
}
```

## innerHTML属性
方便大段替换

## createElement方法
用于创造新的元素
使用方法`document.createElement("nodeName");`

## appendChild方法
用于把新的元素放到html文档中
使用方法`parent.appendChild("child");`

## createTextNode方法
用于创建一个文本节点
使用方法`var txt = document.createTextNode("hello world");`再使用appendChild()即可。

## insertBefore方法
用于把新元素插入到一个元素之前
### 三要素
- 新元素newElement
- 目标元素tragetElement
- 父类元素parentElement
使用方法`parentElement.insertBefore(newElement,targetElement)`

## nextSibling属性
用于获取下一个兄弟元素

## for(key in defs){}
key=nodeValue
[key]=definition

## 用DOM技术访问font-family
错误方法 `element.style.font-family`
正确方法 `element.style.fontFamily`即才用驼峰法访问，但是外部链结样式无法访问(用DOM技术添加的就没问题)
DOM设置style必须要用引号括起来`para.style.color = "black"`

## 设置表格奇数和偶数行样式的方法
```
tr:nth-child(odd){background-color:#ffc;}
tr:nth-child(even){background-color:#fff;}
```

## @import url()
用于把样式表都导入到一个文件中
例如
- layout.css
- color.css
- typography.css  

```
//basic.css
@import url(layout.css);
@import url(color.css);
@import url(typography.css);
```

## HTML DOM form对象
每个form对象都有一个element.length属性，其返回表单中包含的单元个数
