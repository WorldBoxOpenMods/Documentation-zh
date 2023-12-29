# 介绍

这可以说是整个NML里最有技术的一个内容了, 但它的使用方法非常简单. 

你只需要会加一行`[Hotfixable]`, 设置`Config.isEditor=true`, 然后点一下按钮就差不多了.

这个功能一般用来Debug, 考虑这样的一个场景:

```
这里有一个bug, 从游戏开始到这个bug触发需要非常长的一段时间.

这个bug在存读档后就会消失.

这个bug在出现后会保持一段时间.
```

如果采用原始的, 加Log, 然后不断重启游戏来获取信息, 并进行修改测试的方法, 毫无疑问, 会消耗极大量的时间.

如果你使用这个技术, 那么, 你可以暂停游戏, 然后现场修改模组代码并添加log或尝试修复bug, 然后简单地点击重载模组, 即可查看结果.

除此之外, UI设计也是, 在不使用Unity Editor(NeoMod的开发包可以使用Unity Editor进行设计并使用IDE调试模组, 尚未公开, 但C# 8实在不好用), 纯靠代码, 也可以在模组主类的`Reload`中添加对UI组件的摧毁和重新初始化.

# 使用方法

1. 让你的模组主类实现`IReloadable`模组功能接口.
   
2. 运行游戏
3. 遇到问题
4. 给需要修改的函数添加`Hotfixable`特性
5. 修改函数
6. 点击游戏内的模组重载按钮

# 使用示例

视频没录, 等等吧, 上面应该说得很清楚了.

[代码的示例第一部分](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleTraits.cs)

[代码的示例第二部分](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L55)

# 提示

1. `MonoBehaviour`的几个如`Awake`,`Update`等函数无法添加`Hotfixable`特性
2. 构造函数和析构函数不能添加`Hotfixable`特性
3. `Reload`函数本身也能添加`Hotfixable`特性
4. 你可以在游戏运行时给别的函数加上`Hotfixable`
5. 你可以在游戏运行时定义新的函数, 也需要标注`Hotfixable`
6. 匿名函数也可以标注`Hotfixable`进行热更新, 下面所示代码

```csharp
trait.action_special_effect = [Hotfixable] (pTarget, pTile) =>
{
    LogService.LogInfo("Before hotfixed trait action");
}
```
