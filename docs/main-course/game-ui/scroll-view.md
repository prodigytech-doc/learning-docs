# 滚动框

::: tip 阅读本文大概需要 8 分钟。

有时候，我们需要使用容器的功能，但是发现容器内的内容可能过大或过多，容器显示不出来，这时候就需要用到滚动框了，滚动框是一个特殊的容器，可以通过滚动操作来显示超出自身大小的内容，接下来我们就来看下滚动框的使用。

:::

## 1. 创建滚动框

无论是游戏开发还是应用开发，在制作 UI 时，很多时候需要显示的内容会超出我们的显示窗口，比如地图应用、浏览器、记事本、游戏服务器列表等等，那么当遇到这种情况的时候，我们一般都会使用滚动框去解决该问题。滚动框也是一种容器，只是可以通过滚动的方式显示任意大小的内容。

接下来，我们就来创建一个滚动框，双击我们创建的“MyUI”文件打开 UI 编辑器，从“对象”窗口中选中“滚动框”并拖拽到画布中来，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnT85BJ018kOGAjXZ1pJRTPe.png)

## 2. 使用滚动框

在滚动框中添加一个子控件，这里添加一个图片，并保证图片作为滚动框的子物体，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn3JyBaMuMJbOKupSiXtXNyg.png)

多复制几个图片控件，当图片控件超出显示区域后，可以看到滚动条显示出来，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnAY1gtqCVyzT2umQWz4aYkf.gif)

游戏中显示效果如图，可以看到已经在右侧出来了垂直方向的滚动条并支持垂直方向滚动了：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnkpGMtQJnHattrm7DVQTc6c.gif)

## 3. 滚动框属性

在上面我们已经实现了滚动效果了，但是可能展示效果达不到我们的需求，那我们来看下滚动框的常用属性有哪些把，滚动框的“属性面板”如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn5ESzyJoHiG2DMu4GEJRz7f.png)

滚动朝向：设定当前滚动面板是水平方向还是垂直方向。

运动类型：当滚动到边缘的时候是否有反弹效果，默认为反弹效果。

是否有惯性：快速滑动滚动视图后，当手指离开屏幕后，滚动视图是否依然有惯性进行运动。

弹性系数：反弹效果的弹性系数。

显示滚动条：当前滚动条的显示效果设置。

边缘阴影：边缘阴影的显示效果设置。