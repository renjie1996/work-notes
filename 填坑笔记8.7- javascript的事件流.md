# 事件流

事件流是描述对页面接受事件的顺序，IE和Netscape提出了完全相反的事件流模型，描述的是从页面中接收事件的顺序,也可理解为事件在页面中传播的顺序。

** 我们通过平常使用知道addEventListener最后的参数是切换句柄的，当这个布尔值为true时，表示在捕获阶段调用事件处理程序；若果是false，表示在冒泡阶段调用事件处理程序。 **

> MDN：useCapture  可选（）
Boolean，是指在DOM树中，注册了该listener的元素，是否会先于它下方的任何事件目标，接收到该事件。沿着DOM树向上冒泡的事件不会触发被指定为use capture（也就是设为true）的listener。当一个元素嵌套了另一个元素，两个元素都对同一个事件注册了一个处理函数时，所发生的事件冒泡和事件捕获是两种不同的事件传播方式。事件传播模式决定了元素以哪个顺序接收事件。

> Once the propagation path has been determined, the event object passes through one or more event phases. There are three event phases: capture phase, target phase and bubble phase. Event objects complete these phases as described below. A phase will be skipped if it is not supported, or if the event object’s propagation has been stopped. For example, if the bubbles attribute is set to false, the bubble phase will be skipped, and if stopPropagation() has been called prior to the dispatch, all phases will be skipped.

> The capture phase: The event object propagates through the target’s ancestors from the Window to the target’s parent. This phase is also known as the capturing phase.

> The target phase: The event object arrives at the event object’s event target. This phase is also known as the at-target phase. If the event type indicates that the event doesn’t bubble, then the event object will halt after completion of this phase.

> The bubble phase: The event object propagates through the target’s ancestors in reverse order, starting with the target’s parent and ending with the Window. This phase is also known as the bubbling phase.

#### 为什么要使用 addEventListener?
addEventListener 是 W3C DOM 规范中提供的注册事件监听器的方法。它的优点包括：

1. 它允许给一个事件注册多个 listener。当存在其他的库时，使用 DHTML 库或者 Mozilla extensions 不会出现问题。

2. 它提供了一种更精细的手段控制 listener 的触发阶段。（即可以选择捕获或者冒泡）。

3. 它对任何 DOM 元素都是有效的，而不仅仅只对 HTML 元素有效。

## 事件冒泡

IE的事件流叫事件冒泡，逐级向上传播

```html
<html>
    <body>
        <div>
        </div>
    </body>
</html>
```
点击div之后，顺序是div -> body  -> html

## 事件捕获

Netscape事件捕获是与冒泡相反的


## DOM事件流

DOM规定的事件流包括三个阶段
1. 捕获阶段
2. 目标阶段
3. 冒泡阶段

事件捕获阶段，为截获事件提供机会，然后是实际的目标接受事件，最后是事件冒泡阶段

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
  #wrap {
    width: 200px;
    height: 200px;
    background: orange;
  }
  #outer {
    position: relative;
    top: 50px;
    left: 50px;
    width: 100px;
    height: 100px;
    background: #eeddff;
  }
  #inner {
    position: relative;
    top: 25px;
    left:25px;
    width: 50px;
    height: 50px;
    background: #44ddff;
  }

  </style>
</head>
<body>
  <div id="wrap">
    <div id="outer">
      <div id="inner"></div>
    </div>
  </div>
  <script>
    var wrap = document.getElementById('wrap');
    var outet = document.getElementById('outer');
    var inner = document.getElementById('inner');

    wrap.addEventListener('click',function(){
      alert('789');
    },false);
    outer.addEventListener('click',function(){
      alert('456');
    },false);
    inner.addEventListener('click',function(){
      alert('123');
    },false);
    wrap.addEventListener('click',function(){
      alert('wrap');
    },true);
    outer.addEventListener('click',function(){
      alert('outer');
    },true);
    inner.addEventListener('click',function(){
      alert('inner');
    },true);
  </script>
</body>
</html>
```
# 事件的作用范围
事件的作用范围为:
元素自己所占页面空间部分加嵌套元素所占空间范围(若嵌套元素覆盖在容器元素上，则事件的作用范围为容器元素自身所占空间大小)

