# 布娃娃区

## 物体结构

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnr9MXqQbHFNpoS0Nw7Qup6e.png)

## 物体效果

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnKyhyjkA0lwol5oyRrUFzNg.gif)

## 代码示例

```typescript
@Component
export default class TriggerControl extends Script {

    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected async onStart() {
        // 服务端不做任何事
        if (SystemUtil.isServer()) {
            return;
        }

        // 以下为客户端逻辑

        // 获取当前脚本所挂载的触发器
        const trigger = this.gameObject as Trigger
        // 进入触发区域
        trigger.onEnter.add(() => {
            //角色开启布娃娃系统
            Player.localPlayer.character.ragdollEnabled = true;
            //倒计时 3 秒
            setTimeout(() => {
                //角色关闭布娃娃系统
                Player.localPlayer.character.ragdollEnabled = false;
            }, 3000);
        });
    }
}
```

