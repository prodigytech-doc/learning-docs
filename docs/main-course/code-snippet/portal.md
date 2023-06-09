# 传送区

## 物体结构

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcn5vGfmNBrdUYnbaSHbzklAb.png)

## 物体效果

![](https://wstatic-a1.233leyuan.com/productdocs/static/boxcnLuy42wE1XMCmmUvuMinEEh.gif)

## 代码示例

```ts
@Core.Class
export default class TriggerControl extends Core.Script {
    //传送位置
    public position = new Type.Vector(0, 0, 150)

    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected async onStart() {
        //客户端不做任何事
        if(Gameplay.isClient()){
            return
        }
        //以下为服务端逻辑
        //获取当前脚本所挂载的触发器
        let trigger = this.gameObject as Gameplay.Trigger
        //进入触发区域
        trigger.onEnter.add((other: Core.GameObject)=>{
            //2 秒后
            setTimeout(() => {
                //这里判断一下进入区域的物体是不是一名角色
                if(other instanceof Gameplay.Character){
                     //是的话，转成角色类型
                    let character = other as Gameplay.Character
                    //如果是角色，将该角色传送到目标位置
                    character.setWorldLocation(this.position)
                }
            }, 2000);
        })
    }
}
```