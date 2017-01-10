## 说明


知识分享

访问地址 https://spring-fe.github.io/share/


## 动画
### 刷新率
指电子束对屏幕上的图像重复扫描的次数，即屏幕每秒画面被刷新的次数，大多数电脑显示器刷新频率60Hz。
### Javascript动画
#### setTimeout、setInterval
通过setTimeout或setInterval一帧一帧的改变UI达到动画的效果。如果渲染频率与浏览器刷新频率不一致，即延迟时间比刷新时间短，会丢帧，造成视觉上动画卡顿。《图》
#### requestAnimationFrame
对setTimeout、setInterval优化，防止丢帧。每一帧的所有DOM操作集中，一次渲染完成。渲染频率与浏览器刷新频率一致，且对隐藏或不可见元素，不进行重排或重绘。
### GPU加速
直接使用GPU改变图层(UI)，无需渲染引擎重新渲染的过程，提高绘制速度。
如典型的3D变换:
```css
.cube {
   -webkit-transform: translate3d(250px,250px,250px)
   rotate3d(250px,250px,250px,-120deg)
   scale3d(0.5, 0.5, 0.5);
}
```
