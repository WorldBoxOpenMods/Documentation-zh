# 介绍

NML为`ModConfig`提供了友好的用户交互界面, 如下图所示

![ModConfig](../.gitbook/assets/MODCONFIG.png)

[对应的配置文件示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/default_config.json)

对于这样的配置, 你需要你的模组实现`IConfigurable`接口, 并通过`GetConfig`提供一个`ModConfig`实例传递和接收配置信息(当然, 如果你要用这个来实现其他的设置交互也是可以的).

对于BasicMod, 不需要考虑上面那句话, 你只需要在你的模组文件夹下创建一个`default_config.json`文件(ModTemplate已经为你创建好了这个文件), 
并在其中添加/编辑你的配置信息即可.

`default_config.json`故名思意, 提供默认的配置信息, 在加载后会被写入到玩家的长期数据中. 
对于在`default_config.json`中新增的项, NML会自动将其添加到玩家的长期数据中.

# default_config.json编辑

`default_config.json`的格式为[JSON](https://www.runoob.com/json/json-tutorial.html), 你可以使用任何文本编辑器来编辑它.

该文件将会被解析为一个`Dictionary<string, List<ModConfigItem>>`实例, 其中`string`为配置组的名称`groupId`, `List<ModConfigItem>`为从上到下依次排列的配置项.

对于`ModConfigItem`, 你需要提供以下信息:

1. `Id`: 配置项的唯一标识符, 用于在代码中获取配置项的值.
2. `Type`: 配置项的类型, 目前有效的有`SWITCH`(开关), `SLIDER`(滑动条), `TEXT`(文本输入框).
3. `IconPath`: 配置项的图标路径, 将会通过`Resources.Load`进行加载, 路径基于根目录. 如果不需要图标, 则可以不填写此项.
4. `TextVal`: 如果`Type`=="TEXT", 则需填写此项(string), 作为文本输入框的默认值.
5. `FloatVal`: 如果`Type`=="SLIDER", 则需填写此项(float), 作为滑动条的默认值.
6. `BoolVal`: 如果`Type`=="SWITCH", 则需填写此项(bool), 作为开关的默认值.
7. `MinFloatVal`: 如果`Type`=="SLIDER", 则此项(float)有效, 作为滑动条的最小值, 默认为0.
8. `MaxFloatVal`: 如果`Type`=="SLIDER", 则此项(float)有效, 作为滑动条的最大值, 默认为1.
9. `Callback`: 回调函数, 可选项.

对于`Callback`, 你需要定义一个静态函数, 这个函数接受一个参数(该`ModConfigItem`的值类型). 对于这样的`ModConfigItem`:

```json
{
    "Id": "Example",
    "Type": "SLIDER",
    "FloatVal": 0.5,
    "Callback": "ExampleType:ExampleCallbackMethod"
}
```

需要实现这样的函数

```csharp
namespace ANYNAMESPACE;

class ExampleType
{
    void ExampleCallbackMethod(float pUpdatedValue)
    {
        // 你的回调函数代码
    }
}

```

[回调示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleActions.cs)

需要注意的是, 对于模组配置窗口的修改, 会在窗口关闭后一并应用, 而不是在修改时同步.

除此之外, 你还需要为`groupId`和`Id`提供语言文本, 你可以见[多语言文本](Multilingual.md)