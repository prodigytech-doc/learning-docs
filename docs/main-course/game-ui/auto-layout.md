# UI 自适应对齐

::: tip 阅读本文大概需要 5 分钟。

无论是手机还是电脑或者是其他游戏设备，设备屏幕比例与分辨率可谓是百花齐放，低则 4:3，高则 21:9，如此不同的屏幕怎样才能确保我们的 UI 会跟随屏幕不同而自动布局呢？那么自适应功能就可以帮助你解决这个功能！

:::

## 1.什么是自适应

这里演示一下正常开发 UI 中可能存在的一个严重性问题，首先打开 UI 编辑器，在“设计器”窗口中，只保留一个按钮，并放到左下角，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnjTqG3FnjjwTtOPqXIRxuob.png)

这时候如果游戏使用了此 UI，那么根据上图中的画布（屏幕线框）可以看出，按钮会出现在屏幕左下方，并没有什么问题。

这时我们看下上图中的分辨率为 1920x1080，也就是目前我们是使用了该分辨率作为参照进行的 UI 设计，但是当游戏在真机中运行的时候，我们也不能确定真机的分辨率是多少，那么如果这时候我们修改上图中的分辨率为 1920x720，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnnoIL1YH8SR2m3YTUyD3STg.png)

可以在上图中看到，当我们按照 1920x1080 分辨率设计出来的 UI，运行在 1920x720 的手机上的时候，按钮已经出了屏幕，也就是玩家会看不到我们这个按钮，那这就是一个很严重的问题了。

如果我们给按钮一个约束，使按钮无论在多大的分辨率上，都会永远保持在屏幕左下角而不会出屏幕，那就是 UI 的自适应了。

## 2.对齐功能

在 UI 编辑器中，单击选中“Button_1”按钮，可以在“对象属性”窗口中看到该按钮的属性，其中有一项叫做“对齐”，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnBfc43xMBLUGVeGnQ3KoHle.png)

那么水平方向上的“靠左对齐”代表了什么含义呢？其实就表示了当前 UI 控件的左侧相对于父物体的左侧距离为固定不变的。同样，垂直方向上的“靠上对齐”，就表示了当前 UI 控件的上侧相对于父物体的上侧距离为固定不变的，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnKyl2apRppueQhYc8fXhaHf.png)

因为移动设备坐标点（0,0）在左上角，所以可以看出按默认的水平与垂直对齐来看，无论屏幕如何变化，该按钮距离左上角的顶点都是不变的，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnV9lMeAeWlT96e0NexPU2Nc.png)

根据上图可以看出，不同的屏幕分辨率下，按钮的显示位置也不同。

那么如果我们需要让该按钮永远的显示在左下角应该怎么做呢？很简单，我们只需要将垂直方向的对齐设置为“靠下对齐”即可，这样也就是我们的按钮会和屏幕左下角保持固定距离，设置如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnNLJ2Jp0noPoyWrrjlXYeLd.png)

实际效果如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnC5fWc7jY0Cr6anxxUrUDWg.png)

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnx5KMIhzDVzcSlkvysmNYff.png)

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnSZ2LiYUQiM7tkCOC6McQeg.png)

除了距离四个边可以保持固定距离外，也可以设置距离屏幕中心点保持一定的距离，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnn70S8R1noaJDVJ8A2DnRSd.png)

## 3.UI 随分辨率遍布全屏

制作一个 Image

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn3xsujCWJmcX0aqGGzqLRM3.png)

我们设置它的大小与当前分辨率一样

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnfRiV3MPe6m1QN3ZfLPalPb.png)

将对齐方式全设置为自适应

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnNg3EamMvg6t9uS4tfLF0sh.png)

效果如下图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcngQD7eeyx4l8xmK1ZLTbwtP.gif)