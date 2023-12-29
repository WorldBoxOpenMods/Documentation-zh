NML中模组依赖分为硬依赖和软依赖两种

# 硬依赖

也称必需依赖, 只有当所有硬依赖的模组均加载了才会被加载.

硬依赖在`mod.json`中声明硬依赖于某些模组, 而后在项目文件中添加对硬依赖的模组的引用即可(让IDE给出正常的代码分析).

# 软依赖

也称可选依赖, 当软依赖模组不存在时也能被加载. 如果带软依赖模组时编译失败后, 会尝试取消依赖于所有软依赖模组后再次编译.

为了在软依赖的模组缺失时仍能正常编译运行, NML采用宏来控制编译.

当软依赖模组存在时, NML在编译时会加入软依赖模组的ID作为宏, 不存在时则不会添加.

下面的代码是在示例模组(软依赖于"一米_中文名")中, 根据"一米_中文名"模组是否存在来选择添加命名器的方式

```csharp
// 用宏包裹所有"可选"依赖. "一米_中文名"是这个可选依赖的模组id. Chinese_Name是模组"一米_中文名"提供的命名空间.
using System.IO;
#if 一米_中文名
using Chinese_Name;
#endif

namespace ExampleMod.Content;

internal static class ExampleNameGenerators
{
    public static void init()
    {
        // 如果模组"一米_中文名"被编译, 初始化中文名生成器. 否则, 初始化原版名字生成器.
#if 一米_中文名
        init_chinese_name_generators();
#else
        init_vanilla_name_generators();
#endif
    }
#if 一米_中文名
    private static void init_chinese_name_generators()
    {
        // 因为下面的方法和类是由模组"一米_中文名"提供的, 你应该用宏包裹它们.
        WordLibraryManager.SubmitDirectoryToLoad(Path.Combine(ExampleModMain.Instance.GetDeclaration().FolderPath,
            "additional_resources/word_libraries"));
        CN_NameGeneratorLibrary.SubmitDirectoryToLoad(Path.Combine(ExampleModMain.Instance.GetDeclaration().FolderPath,
            "additional_resources/name_generators"));
    }
#endif
    private static void init_vanilla_name_generators()
    {
        // 暂时没有内容
    }
}
```

在IDE中, 你也需要添加对依赖模组的引用, 除此之外, 你还需要在项目文件中添加模组ID为预定义常量(这一行都是针对你要使用完整IDE功能的情况)

[相关示例代码](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleNameGenerators.cs)

[mod.json配置示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/mod.json)

[预定义常量配置示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleMod.csproj#L21)

# 如何添加对依赖模组的引用

[相关示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleMod.csproj#L66)

## DLL引用

引用在`worldbox_Data/StreamingAssets/mods/NML/CompiledMods`中, 名为对应模组ID的.dll文件

## 项目引用

如果发布的依赖模组中包含了项目文件, 可以直接引用依赖模组的项目文件.