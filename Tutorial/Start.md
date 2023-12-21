---
description: 基础配置--劝退的开始
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

在这一节, 配置开发环境.

# 人

1. 你需要是一个智力完备且拥有独立思考能力的人
2. 为了更好地解决你会遇到的问题, 建议先阅读[提问的智慧](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way/blob/main/README-zh\_CN.md)
3. 然后你需要掌握[最基础的CSharp知识](https://www.runoob.com/csharp/csharp-tutorial.html)
4. 如果可以的话, 推荐掌握[最基础的Git用法](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)



# 基础环境

* 游戏本体
* 安装NeoModLoader



# 代码编辑器

下面有几种可选的, 按推荐程度排序:

1. `Rider`. 付费, 但可以学生认证/开源项目
2. `Visual Studio Community`. 免费
3. `Visual Studio Code`. 免费, 轻量, 但配置对于新手较麻烦
4. `记事本`. 免费, 轻量, 无需配置, 就是蠢



# 查看游戏源码

这里推荐两者同用, 恰好互补

* `ILSpy` 能够得到高可读的代码, 并且能够导出符号文件(.pdb)
* `DnSpy` UI好看, 悬停在按钮上有高亮(ILSpy没有), 查看IL代码时能够看到指令index



# 查看游戏资源

* `AssetRipper` 能够将游戏导出为Unity工程文件



# Debug

* `BepInEx` 并开启`BepInEx\config\BepInEx.cfg`中`Logging.Console` `Enable`项, 原版的控制台太难用了, 这个选中其中文本能够冻结游戏.
* `UnityExplorer` 一个BepInEx插件
* IDE调试开发包(包含了所有游戏源码和资源, 暂不开放)

# 示例代码

现在的一些开放的NeoMod代码仓库

* [ModExample](https://github.com/WorldBoxOpenMods/ModExample/) 一个纯粹的示例代码仓库, 将会包含该文档几乎所有功能的示例代码
* [中文名](https://github.com/WorldBoxOpenMods/ChineseName) 
* [启源核心](https://github.com/inmny/Cultivation-Way-Core) 一个大型模组, 如果只是为了找代码示例, 不推荐看这个