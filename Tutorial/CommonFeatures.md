# 对于BasicMod

## 日志

`BasicMod`提供了`LogInfo`, `LogWarning`, `LogError`三个静态函数来打印日志, 会带上模组名称的前缀

## 实例

`BasicMod`提供了`Instance`静态属性可以直接访问模组主类的实例

## 模组信息

`BasicMod`提供了`GetDeclaration`能够获取模组声明信息(`ModDeclare`, 不是`ModDeclaration`, 这个名给可恶的NCMS用作命名空间了, 为了方便代码编写, 故改名), 包括模组名, 所在文件夹等, 具体定义如下

```csharp
// 部分字段不在此处展示, 具体见 `基础概念/模组声明`
public class ModDeclare
{
    // 模组名
    public string Name { get; private set; }
    // 模组ID
    public string UID { get; private set; }
    // 作者
    public string Author { get; private set; }
    // 版本
    public string Version { get; private set; }
    // 描述/简介
    public string Description { get; private set; }
    // 仓库地址
    public string RepoUrl { get; private set; }
    // 必需依赖
    public string[] Dependencies { get; private set; }
    // 可选依赖
    public string[] OptionalDependencies { get; private set; }\
    // mod.json文件所在文件夹路径
    public string FolderPath { get; private set; } = null!;
    // 图标路径(相对于mod.json文件所在文件夹路径)
    public string IconPath { get; private set; }
}
```

`BasicMod`提供了`GetLocaleFilesDirectory(ModDeclare)`能够直接获取本地化文件所在文件夹路径. 传入`GetDeclaration`的结果作为参数.

## 模组设置

`BasicMod`默认是一个提供设置界面的Mod, 你可以通过`GetConfig`来获取`ModConfig`实例, 具体用法见[模组设置](../BasicConcept/ModConfiguration.md)

## 多语言

在模组文件夹下创建`Locales`文件夹, 参考`ModTemplate`中的写法即可. 目前仅支持json和csv文件.

# 其他常用特性

## 日志

`NeoModLoader.services.LogService`提供了

* 一般的`LogInfo`,`LogWarning`,`LogError`三件套,
* 打印调用堆栈的`LogStackTraceAsInfo`, `LogStackTraceAsWarning`, `LogStackTraceAsError`
* 在多线程情况下使用的`LogInfoConcurrent`, `LogWarningConcurrent`, `LogErrorConcurrent`.

## 贴图

在模组文件夹下创建一个名为`GameResources`的文件夹, 其中的`.png`,`.jpg`,`.jpeg`会由对应的`.meta`文件或`sprites.json`文件解释然后加载进游戏, 可以通过`Resources.Load`, `SpriteTextureLoader.getSprite`相关函数进行加载. 具体见[模组资源概览](../ModResources/Overview.md).

`NeoModLoader.utils.SpriteLoadUtils`提供了

* `LoadSingleSprite(string)`来加载指定系统路径下的图片文件
* `LoadSprites(string)`搜寻相关联的`.meta`文件(解释为一个`TextureImporter`, 并提供了一个`SpriteSheet`)或`sprites.json`来加载路径下的图片文件

## 模组名/作者/简介多语言

如果要你的模组在英文环境下 模组名/作者/简介显示为英文(en)，则需要添加本地化文本，相应的key为:

1. `模组名_en`
2. `作者_en`
3. `简介_en`

## AssetBundle拓展

`NeoModLoader.utils.AssetBundleUtils`提供了加载`AssetBundle`文件为`WrappedAssetBundle`的方法(同时避免重复加载).

`NeoModLoader.utils.WrappedAssetBundle`提供了类似`Resources.Load`, `Resources.LoadAll`的方法来加载资源