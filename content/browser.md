
## 浏览器渲染原理及拓扑图实现
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

## setTimeout
* 延迟指定的时间把任务放入执行队列
* javascript空闲时，执行队列任务
* 改变UI显示
* 延迟时间比刷新时间短，丢帧，卡顿

---

## requestAnimationFrame
* 对setTimeout优化，防止丢帧
* 每一帧的所有DOM操作集中，一次渲染完成
* 渲染频率与浏览器刷新频率一致
* 对隐藏或不可见元素，不进行重排或重绘
* 不支持，封装

---

## webWorker
* 在浏览器后台运行javascript
* 与dom无关操作

---

## 主线程与合成线程
* 协同工作渲染网页
* 可同步

---

## 主线程
* 解释javascript
* 渲染线程

  * 计算HtML元素的CSS样式
  * 页面布局
  * 将元素绘制到一个或多个位图中
  * 把位图交给合成线程
* javascript线程与渲染线程互斥

---

## 合成线程
* 通过GPU将位图绘制到屏幕
* 通知主线程更新页面中可见或即将变成可见的部分位图
* 计算出页面中哪部分是可见的
* 计算出当你在滚动页面时哪部分是即将变成可见的
* 当你滚动页面时将相应位置的元素移动到可视区域

---


## 图层(层叠上下文)（chrome)
* 浏览器渲染页面时，将页面分为多个图层
* 图层有大有小
* 每个图层上有一个或几个节点

---

## 图层（层叠上下文）产生
* 根元素(html)
* 绝对定位或相对定位且z-index值不为auto
* flex-item,且z-index不为auto
* 元素的opacity属性值小于1
* 元素的transform属性值不为none
* position: fixed
* 元素的-webkit-overflow-scrolling值为touch
* ...

---

## 图层特点
* 独立的图层，不重排
* transform、固定定位元素

---


## 浏览器工作过程
* 获取DOM后分割为多个图层
* 对每个图层的节点计算样式结果(Recalculate style)
* 为每个节点生成图形和位置(Layout)
* 为每个节点绘制填充到图层位图中(Paint)
* 图层作为纹理上传至GPU
* 重组多个图层到页面上生成最终屏幕图像(Composite Layers)

---

## GPU绘制
* 直接使用GPU改变UI, 无需渲染引擎处理
* 提高绘制速度
* 2D transform

---

```markup
@-webkit-keyframes imgSmall{
	0%{
		-webkit-transform:scale(1);
	}
	100%{
		-webkit-transform:scale(0.5);
	}
}
```

---

## 2d transform  与 3d transform
* 都是GPU直接操作图层，建立动画
* 页面渲染前，3D动画创建独立的复合图层
* 在运行期间，2D动画创建一个独立图层
* 2d动画，两次repaint操作（运行时产生图层，结束后删除图层)
* 3d动画，不需要repaint


---

## GPU加速

---


## opacity与rgba

* opacity

    * 先渲染整体颜色，再进行透明度计算
    * opacity占一个图层
    * 通过GPU改变元素整个图层透明度
    * 无需重排、重绘

* rgba
	* 渲染最后结果值
	* 使用alpha对前3个值分别进行透明计算
	* 渲染器对三个颜色进行合并计算