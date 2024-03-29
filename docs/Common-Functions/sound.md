# 音效

::: tip 阅读本文大概需要 10 分钟。

音效是一种很重要的内容表现手法，在音乐、影视与游戏中，音效可谓是无处不在。在一部优秀的游戏中，恰当的音效可以让游戏的场景与剧情更加生动，在游戏开发中一定要认真搭配合适的音效。

:::

<iframe sandbox="allow-scripts allow-downloads allow-same-origin allow-popups allow-presentation allow-forms" frameborder="0" draggable="false" allowfullscreen="" allow="encrypted-media;" referrerpolicy="" aha-samesite="" class="iframe-loaded" src="//player.bilibili.com/player.html?aid=322817180&bvid=BV1qw411q7ba&cid=1317940823&p=18&autoplay=0" style="border-radius: 7px; width: 100%; height: 360px;"></iframe>

了解更多本节内容见产品文档：[音效 | 产品手册 (ark.online)](https://docs.ark.online/GameplayObjects/SoundEffect.html)

## 1. 什么是音效

这里的音效包含：音乐和音效。音乐通常指持续时间比较长的声音，例如游戏在每个场景中都会循环播放的背景音乐；音效通常指瞬间的声音效果，例如脚步声、射击声、碰撞声等。编辑器中将音效分为 **2D 音效**（全局音效，类似把音箱放在人的身上，人不管在哪里都是听到一样的声音大小）和 **3D 音效**（空间化，类似把音箱放到地上固定，人走远声音就变小，近点声音就变大）。

下列举几个音效场景便于理解：

- 界面音效

  - 用于界面操作的音效，界面音效贯穿整个游戏过程，比如菜单弹出收回、鼠标选定，物品拖动等等，可使用 2D 音效。
- NPC 音效

  - 所有角色相关音效，比如脚步声、跑步声、死亡声、被攻击的叫声等等，可使用 3D 音效。
- 环境音效

  - 自然环境声，比如风声、湖水涟漪的轻声、瀑布声、鸟鸣等等，可使用 3D 音效。
- 技能音效

  - 主要指各种攻击声音、刀的舞动、矛的冲刺、踢、打、爆炸等音效，可使用 2D / 3D 音效。
- 背景音效

  - 主要指游戏中不同场景，不同地图的音乐，比如不同地图搭配不同风格的音乐，回合制游戏中战斗场景中的战斗配乐等，可使用 2D 音效。

## 2. 音效属性

在“本地资源库”中找一个音效文件，拖拽到场景中，如图：

![Twq23fKUYjd1694600961](https://arkimg.ark.online/Twq23fKUYjd1694600961.webp)

可以看到声音拖拽到场景中后，会生成两个球体边框，也就是默认音效为 3D 音效，其中小球体内部音量不会衰减，而小球体外到大球体之间的空间会产生衰减，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnqBbEAcJKtjMQWRBBg7k9rb.png)

接下来选中我们的声音对象，看一下包含了哪些可设置的属性，如图：

![BFSuVAfUppb1694601263](https://arkimg.ark.online/BFSuVAfUppb1694601263.webp)

① 播放按钮：播放预览音频。

② 自动启用、循环播放、音效空间化。

* 自动启用：游戏启动时是否自动播放该音频。

* 循环播放：是否循环播放。
* 音效空间化：是否设置为 3D 音效，3D 音效和 2D 音效区别：
  * 3D 音效：会随距离远近而有音量大小的变化，且戴耳机时可以明显听出来该音效播放的位置，具有 3D 空间效果。
  * 2D 音效：在任何位置都可以听到同样的音量大小，且不会有空间效果。

![DZx0zS36TM81694601628](https://arkimg.ark.online/DZx0zS36TM81694601628.webp)

③ 音效形状以及对应形状的设置（**仅开启音效空间化时生效**）
* 音效形状：球形、胶囊体、盒体、锥体。
* 不同形状区域，代表音效的扩散&衰减的区域不同，实际使用需要根据游戏效果决定用什么形状。

④ 衰减距离（**仅开启音效空间化时生效**）：离得越远声音越小，这个距离可以远到什么位置，通过衰减距离来进行配置。

⑤ 音量比例：就是声音大小，0 ~ 1 代表百分比，从 0 ~ 100%。

## 3. 播放音效

![VIYt8EQ8WN61694601566](https://arkimg.ark.online/VIYt8EQ8WN61694601566.webp)

勾选“启用”

勾选“循环播放”（这里测试效果是避免音效太短运行起来没听见）

运行游戏，就可以听到声音按照上面的属性设置播放了起来！

## 4. 动态播放音效

有时候我们不想将声音拖到场景中直接播放，而是希望完全通过脚本播放声音，这时候我们可以通过脚本来先加载音效再进行播放。

首先找到想播放的音效，右键单击，在菜单中复制音效的 资源ID，如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcntyRF0TVsKoI9wFrjOfmyOb.png)

新建一个脚本，这里命名为 `SoundControl`，并将其挂载到对象列表上（注意，**一定要挂载脚本**），如图：

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnECrxU0NJCZc644WaZG6lag.png)

双击打开脚本编写代码，使用 `SoundService` 来播放音效，如下：

```typescript
@Component
export default class SoundControl extends Script {
    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected onStart(): void {
        if (SystemUtil.isClient()) {
            // 播放音效 id 为 118362 的背景音乐
            SoundService.playBGM("118362");
        }
    }
}
```

保存脚本，运行游戏，就可以听到声音按照上面的属性设置播放了起来！

另外 `SoundService` 除了播放背景音乐的函数，也提供了其它播放 3D 音效的函数和 2D 音效的函数，都可以尝试下：

```typescript
// 播放背景音乐，assetId 为资源 id，volume 为音量大小 0-1-volume 可不传
SoundService.playBGM(assetId, volume)

// 播放 3D 空间音效，assetId 为资源 id，target 为想播放到哪个位置,可以直接传对象的GameObjectID、对象、坐标，loopNum 为循环次数，volume 为音量大小 0-1
SoundService.play3DSound(assetId, target, loopNum, volume)

// 播放 2D 音效，assetId 为资源 id，loopNum 为循环次数，volume 为音量大小 0-1
SoundService.playSound(assetId, loopNum, volume)
```



## 5. 预览音效效果

除了刚才拖到场景里面的音效属性面板可以预览音效以外，还可以直接在资源库预览音效。

在具体音效资源的右上角，有一个 + 号按钮(如果是下载按钮就点击一下资源就会自动下载)，点击后会弹出一个预览窗口，该功能能为我们省去拖入场景听音效的时间

<video controls="" src="https://arkimg.ark.online/V3MTqlVRWbbsEL7f.mp4"></video>

* 在预览窗口中会有一个播放按钮，点击即可播放音效来预览
* 除此以外，还有一个**预览多个音效**的便利操作：
  * 在点击预览窗口的情况下，不关闭预览窗口，直接再点击左边资源库的其他音效，即可直接切换音效预览。
  * 点击其他音效预览之后，键盘上的上下左右按键也可以切换其他音效的哦