# 数据持久化

::: tip 阅读本文大概需要 6 分钟。

很多时候，我们需要将游戏中玩家的积分、等级、位置等信息储存下来，当玩家下次登录可以进行数据读取以便玩家继续游玩而不用重新开始，MW 提供了非常简单的数据持久化接口，使用后可以轻松将数据存储到服务器中而不用担心丢失等问题！

:::

更多数据持久化见产品文档：[数据存储](https://docs.ark.online/Scripting/DataStorage.html)

## 1. 通用数据持久化

有些时候我们需要将一些通用数据保存到服务器，方便我们下次登录游戏后可以取值，通用数据代表该数据不属于任何玩家，例如游戏运行时间、玩家积分排行榜、场景机关状态等等，这些数据就需要在游戏结束前同步到服务端，在下次登录时候读取进行加载。

口袋方舟编辑器中使用数据存储非常简单，示例代码如下：

```ts
@Core.Class
export default class DataTest extends Core.Script {

    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected onStart(): void {
        //储存数据只在服务端生效
        if(Util.SystemUtil.isServer()){
            //保存数据 参数 1：保存数据的 key， 参数 2：需要保存的内容
            DataStorage.asyncSetCustomData("score", 100).then(state=>{
                //判断是否储存成功
                if(state == DataStorage.DataStorageResultCode.Success){
                    console.log("数据储存成功")
                } else {
                    console.log("数据储存失败")
                }
            })

            //5 秒后，读取数据
            setTimeout(() => {
                 //保存数据 参数 1：保存数据的 key
                DataStorage.asyncGetCustomData("score").then(score=>{
                    console.log("读取数据成功")
                    console.log(score)
                })
            }, 5000);
        }
    }
}
```

## 2. 玩家数据持久化

在我们开发游戏的过程中，除了通用数据需要保存外，常常还要保存每个玩家自己的数据，例如需要保存每名玩家的角色名称、血量、金钱、装备、状态等等，这时候使用通用数据持久化方式进行储存就会有些复杂，口袋方舟为我们提供了一个玩家数据存储的专用 API，使用方法与通用类似，只是需要多传递一个玩家对象，来表示该数据为谁而存，具体使用示例如下：

```ts
@Core.Class
export default class DataTest extends Core.Script {

    /** 当脚本被实例后，会在第一帧更新前调用此函数 */
    protected onStart(): void {
        //储存数据只在服务端生效
        if(Util.SystemUtil.isServer()){
            //等待 5 秒
            setTimeout(() => {
                //从当前所有客户端中，获取一名客户端玩家作为示例
                let player = Gameplay.getAllPlayers()[0]
                //保存数据 参数 1：保存数据的玩家， 参数 2：需要保存的内容
                DataStorage.asyncSetPlayerData(player, 99).then(state=>{
                    //判断是否储存成功
                    if(state == DataStorage.DataStorageResultCode.Success){
                        console.log("数据储存成功")
                    } else {
                        console.log("数据储存失败")
                    }
                })

                //5 秒后，读取数据
                setTimeout(() => {
                    //保存数据 参数 1：保存数据的玩家
                    DataStorage.asyncGetPlayerData(player).then(score=>{
                        console.log("读取数据成功")
                        console.log(score)
                    })
                }, 5000);
            }, 5000);
        }
    }
}
```

::: warning 注意

数据存储只支持基本数据类型，如只能存 Number、string、Array 等，不支持存储自定义函数、Map 等。

:::