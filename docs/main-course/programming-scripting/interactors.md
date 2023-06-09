# 交互物

::: tip 阅读本文大概需要 10 分钟。

配合触发器，交互物可以让开发者快速的制作带有交互行为功能的物体，例如坐到椅子上、开门、开机关等，接下来我们就来一起制作一个交互物吧。

:::

了解更多本节内容见产品文档：[交互物](https://docs.ark.online/GameplayObjects/Interactors.html)

## 1. 什么是交互物？

交互物可以让开发者快速的制作带有交互行为的功能。

**一些使用场景**

例如：坐椅子、开门等，或者是看风景等（cf 挑战中固定的加特林）

## 2. 如何使用交互物

![](https://cdn.233xyx.com/1681133087136_709.PNG)

在编辑器左下角【游戏功能对象】选项中，找到【逻辑对象】，点击其中的【交互物】，拖拽到主视口。

![](https://cdn.233xyx.com/1681133214660_810.PNG)

在【对象管理器】中点击交互物，【属性面板】中就可以出现交互物的属性面板，可以修改交互物的交互姿态，这里修改为 4175，是一个坐下姿态。

![](https://cdn.233xyx.com/1681133086983_238.PNG)

由于交互对象自身不带触发逻辑，所以添加触发器到场景，然后写如下代码：

```ts
@Core.Class
export default class Launch extends Core.Script {
    //填写触发器的 guid
    triggerGUID = "BECDF9554347D0D403E6019242FE28B6"
    //填写交互物的 guid
    interactiveGUID = " 65C6E28F464C53AD49BAFE86BD7B1F36"
    
    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected async onStart() {
        //因为是坐下是个动作，我们只需要在客户端表现，这里就在客户端运行
        if(Util.SystemUtil.isClient()){
            //下载并加载 4175 资源
            await AssetUtil.asyncDownloadAsset("4175")
            AssetUtil.loadAsset("4175")
            //获取交互物
            let interactive = (await Core.GameObject.asyncFind(this.interactiveGUID)) as Gameplay.Interactor
            //获取触发器
            let trigger = (await Core.GameObject.asyncFind(this.triggerGUID)) as Gameplay.Trigger
            //触发器事件绑定
            trigger.onEnter.add(go=>{
                // 判断进入碰撞区域的对象是否为角色
                if (!(go instanceof Gameplay.Character)) {
                    // 不是角色，停止执行
                    return;
                }
                // 进入的对象转为角色类
                let char = go as Gameplay.Character;
                //让该角色进入交互
                interactive.enterInteractiveState(char)
                //离开交互，并移动到某个位置
                //nteractive.exitInteractiveState(Type.Vector.zero)
            })
        }
    }
}
```

## 3. 演示效果

![](https://cdn.233xyx.com/1681133087086_233.gif)

::: warning 注意事项

1. 交互对象的缩放没有实际意义，请使用位置、旋转对其进行编辑，交互对象的旋转通常会改变角色姿态动画的旋转
2. 交互对象自身不带触发逻辑，所以通常情况下你还需要一个触发条件，这个条件可以是其他的触发条件，如按下某键
3. 交互物是一个双端对象，生成的时候需要在双端生成，激活交互和离开交互都在客户端进行。
4. 交互物的 guid 为 Interactor
5. 代码中获取交互物类型为 Gameplay.Interactor。
6. 需要为你在交互物中填写的姿态 guid 添加到属性 preloadAssets 中。

:::