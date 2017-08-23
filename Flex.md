# CSS Flex学习笔记
## 简介
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
### 兼容性
![image](https://user-gold-cdn.xitu.io/2017/8/20/54272308d484c291a12805e55a5bbb42?imageView2/0/w/1280/h/960)
## 知识清单
> 一、webkit问题：记得 Webkit 内核的浏览器，必须加上 -webkit 前缀

> 二、设为 Flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。

> 三、两根轴你要知道是什么：

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

> 四、属性需要使用好：

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

---

**flex-direction：方向**

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

*row | row-reverse | column | column-reverse*


---

**flex-wrap:轴线排不下怎么办？换行？**

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071006.png)

*flex-wrap: nowrap | wrap | wrap-reverse;*

**1. 打死不换行 nowrap**

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)


**2. 换行，第一行在上方。wrap**
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

**3. 换行，第三行在下方。wrap-reverse**
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)

---
**flex-flow** 融合前两者


```css
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

---

**重点来了：主轴justify-content属性**

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)
它可能取5个值，具体对齐方式与轴的方向有关。假设主轴为从左到右。

- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
---
**align-item交叉轴**

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为- auto，将占满整个容器的高度。


---
**align-content属性**

需要两轴都有对齐时

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。