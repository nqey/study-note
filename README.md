# 什么是组件化
## 组件化目的
大型团队的协同合作
## 组件化的缘由
1. 几乎所有的码农写代码,都以自我为中心
2. JS是单线程的，CSS是全局的, 几个人一起搞，一个bug全家玩完
## 解决方案
### 内聚性
你怎么写代码我不管，你的功能全在这你这儿实现
### 低耦合性
你代码不要block(影响)我的代码

## 解决方案衍生的框架
>YUI,ExtJS,web component
## web component
#### 1. 影子DOM (shadow dom)   
　　使用控件的时候并不关心控件的内部结构，只关心控件的本身，所以需要一种方式来将内部的信息封装起来。    
特定场合才能看见的结构，方便DOM遍历 比如video标签   
创建Shadow DOM ： 通过 createShadowRoot 函数对一个 DOM 元素（宿主元素）创建一个 Shadow DOM 子树   
    
　　渲染影子DOM的div的样式，使用(Pseudo Selector)伪类选着器. 
```
  video::-webkit-media-controls-panel{    
        background-color: red;    
  }
```
#### 2. 自定义元素（Custom Elements）   
* 注册：有生命周期 有自己的脚本行为和CSS样式。它们是Web组件的一部分，但也可以自己单独使用。    
  1. 创建对象   
  2. 定义对象属性   
  3. 定义生命周期方法   
  4. 注册新元素    
* 非注册：没有生命周期。   
#### 3. template
　　用于保存客户端内容的机制，该内容在页面加载时不被渲染，但可以在运行时使用JavaScript进行实例化。    
可以将一个模板视为正在被存储以供随后在文档中使用的一个内容片段。    
在加载页面的同时,解析器会处理 <template>元素的内容，但只是确保这些内容是有效的; 元素的内容不会被渲染。    
创建一个template的 html 标签，通过 javascript 获取节点的模板内容   
    
　　模板默认不显示，需要激活模板，通过以下两种方法来激活节点    
　　1. 克隆节点:
```
　　var templateContent  = template.content;
　　var activeNode = templateContent.cloneNode(true);
　　document.body.appendChild(activeNode);
```
　　2. 导入节点
```
　　var templateContent  = template.content;
　　var activeNode = document.importNode(templateContent,true);
　　document.body.appendChild(activeNode);
```
#### 4. import
Html Import 可以将外部的 HTML 文档嵌入到当前文档中，提供很好的资源共享        
带有import属性的link 支持两个事件      
onload：文件成功引入页面会触发      
onerror： 文件加载失败会触发      
#### 例
```
　　<link rel="import" href="banner.html">
　　<link rel="import" href="phones.html">
　　<link rel="import" href="list.html">
　　<template name="t-listBox">
    　　<t-banner></t-banner>
    　　<t-phone></t-phone>
    　　<t-list></t-list>
　　</template>
```