---
title: sass学习笔记
date: 2016-11-13 11:43:03
tags: sass
categories: sass
---
***
## 文件后缀名
统一使用.scss，区分大小括号

## 默认变量
在末尾加入`!default`即可,
例如`$baseLineHeight: 1.5 !default;`
sass的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可
```
$baseLineHeight:        2;
$baseLineHeight:        1.5 !default;
```
<!-- more -->
## 多值变量
1. list
list数据可通过空格，逗号或小括号分隔多个值，可用nth($var,$index)取值。
```
    $linkColor:         #08c #333 !default;//第一个值为默认值，第二个鼠标滑过值
    a{
      color:nth($linkColor,1);
      &:hover{
        color:nth($linkColor,2);
      }
    }
```
2. map
map数据以key和value成对出现，其中value又可以是list。格式为：$map: (key1: value1, key2: value2, key3: value3);。可通过map-get($map,$key)取值。
```
    $headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
    @each $header, $size in $headings {
      #{$header} {
        font-size: $size;
      }
    }
```

## 全局变量
在变量值后面加上!global即为全局变量。这个目前还用不上，不过将会在sass 3.4后的版本中正式应用。目前的sass变量范围饱受诟病，所以才有了这个全局变量。

## 目前变量机制
在选择器中声明的变量会覆盖外面全局声明的变量。(这也就人们常说的sass没有局部变量)

## @at-root
跳出选择器嵌套
```
//sass style
//-------------------------------
//没有跳出
.parent-1 {
  color:#f00;
  .child {
    width:100px;
  }
}
//单个选择器跳出
.parent-2 {
  color:#f00;
  @at-root .child {
    width:200px;
  }
}
//多个选择器跳出
.parent-3 {
  background:#f00;
  @at-root {
    .child1 {
      width:300px;
    }
    .child2 {
      width:400px;
    }
  }
}
```
@at-root (without: …)和@at-root (with: …)
默认@at-root只会跳出选择器嵌套，而不能跳出@media或@support，如果要跳出这两种，则需使用@at-root (without: media)，@at-root (without: support)。这个语法的关键词有四个：all（表示所有），rule（表示常规css），media（表示media），support（表示support，因为@support目前还无法广泛使用，所以在此不表）。我们默认的@at-root其实就是@at-root (without:rule)。
