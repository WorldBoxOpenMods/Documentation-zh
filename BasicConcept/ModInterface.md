# 介绍

## 模组主类接口

### 与NCMS的不同点

与NCMS的`ModEntry`特性来表示模组入口不同, NML用`IMod`接口来表示一个模组主类.

并不是为了和NCMS做区分, 通过接口的方式能够在保证模组设计统一的情况下保证coding的自由, 以及模组的可拓展性.


### 与NCMS的相同点

模组的主类除了需要实现`IMod`接口外, 还需要继承`MonoBehaviour`.

## 模组其他功能接口

除了表示模组主类的`IMod`以外, NML还提供了`IConfigurable`(提供设置), `ILocalizable`(自动多语言处理), `IReloadable`(热更新), `IUnloadable`(可卸载), ...(后续可能会继续添加)等功能性的接口.

## 常用接口打包

这么多接口, 一个个实现太麻烦了, [`BasicMod`](../Packed/BasicMod.md)欢迎你. 打包实现了`IMod`, `IConfigurable`, `ILocalizable`, 并提供了一些有用的函数.

[相关示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L11)

# IMod

通常用于模组主类, 在实现`IMod`接口外, 还需要继承`MonoBehaviour`(除非你有想法做子模组).

`IMod`需要实现以下四个函数

```csharp
/// <summary>
/// 获取模组声明, 仅会在OnLoad之后被调用(忘了还有接口属性)
/// </summary>
public ModDeclare GetDeclaration();
/// <summary>
/// 获取模组实例的gameObject, 仅会在OnLoad之后被调用(忘了还有接口属性)
/// </summary>
public GameObject GetGameObject();
/// <summary>
/// 获取模组页面/仓库URL, 可以直接通过模组声明中的RepoURL获取
/// </summary>
public string GetUrl();
/// <summary>
/// 这个函数会在模组加载时被调用, 会早于Awake, Start, OnEnable等
/// </summary>
/// <param name="pModDecl">属于该模组的模组声明</param>
/// <param name="pGameObject">该模组的GameObject实例(一般用不到)</param>
public void OnLoad(ModDeclare pModDecl, GameObject pGameObject);
```


# IConfigurable

当一个模组主类实现了`IConfigurable`, 那么就可以在模组列表里看到这个模组的模组设置的入口按钮.

相应的, 你需要实现下面这个函数

```csharp
/// <summary>
/// 这个函数会晚于OnLoad被调用, 你需要返回一个ModConfig实例, 你可以临时创建, 也可以读取文件
/// </summary>
public ModConfig GetConfig();
```

`ModConfig`相关具体见[模组设置](./ModConfiguration.md)

# ILocalizable

当一个模组主类实现了`ILocalizable`, 那么就会自动在模组`OnLoad`加载前为其加载本地化文本(.csv和.json两种格式). 貌似没什么用,

相应的, 你需要实现下面这个函数
```csharp
/// <summary>
/// 通过pModDelcare获取要自动加载的本地化文件所在的文件夹路径
/// </summary>
/// <returns>要自动加载的本地化文件所在的文件夹路径</returns>
public string GetLocaleFilesDirectory(ModDeclare pModDeclare);
```

# IReloadable

当一个模组主类实现了`IReloadable`, 并且在`Config.isEditor=true`的情况下, 在模组列表里可以看到该模组的重载按钮.

限制`Config.isEditor=true`是为了避免在玩家误触模组重载按钮而导致不知名的异常.

相应的, 你需要实现下面这个函数

```csharp
/// <summary>
/// 这个函数会在点击重载按钮, 并完成函数的热更新后被调用
/// 由于unity(用nmd 2020版)的限制, 你需要自己控制重载的内容
/// </summary>
public void Reload();
```

除此之外, NML还提供了`Hotfixable`特性, 作用于函数上, 能够标记一个函数在重载前被热更新. 更具体的详见[模组重载](../AdvancedTech/ModReload.md)

# IUnloadable

当一个模组主类实现了`IUnloadable`, 在模组列表里点击模组按钮禁用模组时会直接调用其卸载函数将模组"卸载"(并不是完全意义上的卸载, 只是让模组自己将内容给卸了). 应该没有人闲的要用这个吧.

你需要实现下面这个函数
```csharp
public void OnUnload();
```