
## 浏览器渲染原理及D3
### by spring
#### 2016

---

## 浏览器渲染过程－渲染引擎
单线程

![](images/browser/browser-work.png)

---

## 浏览器渲染过程－DOM
```markup
<html>
	<head>
		<title>Web page parsing</title>
	</head>
	<body>
		<h1>Web page parsing</h1>
		<p>This is an example Web page.</p>
	</body>
</html>
```

---

## DOM树
![](images/browser/dom.png)

---

## 浏览器渲染过程－Javascript引擎
* 处理交互，操作DOM
* 单线程，避免处理UI冲突


---

## Javascript引擎－异步
* 事件click,keyup...(事件触发线程)
* setTimeout(func,delay)(计数器触发线程)
* ajax请求(http请求线程)

![](images/browser/queue.png))

---

## Javascript线程与渲染线程互斥
```html
<ul id="myList">
	<li>tab1</li>
	<li>tab2</li>
	<li>tab3</li>
</ul>
```
```js
var list = document.getElementById("myList");
list.removeChild(list.childNodes[0]);

var a = 1;
```

---

## SVG
* 可缩放矢量图形(Scalable Vector Graphics)
* 形状元素
	* <rect> 矩形
	* <circle> 圆
	* <line> 直线
	* ...

---

## D3.JS
* 数据驱动文档(Data-Driven Documents)
* Javascript库，数据可视化
* 核心思想：把数据与元素绑定在一起，根据数据操作DOM
![](images/browser/d3.png)

---

## D3-画圆形
```js
var data = 10;
circle.datum(data);

circle
.attr("x",20)
.attr("y",20)
.attr("r",function(){
	return d3.select(this).datum();
})
```
第一行data变量赋不同的值，下面的代码不用修改，即可画出不同半径大小的圆

---
