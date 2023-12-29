# 介绍

NML与NCMS一样, 用`mod.json`文件来表示一个模组的信息. 但不同的是, NML用`mod.json`来定位模组, 如果一个文件夹中不存在一个有效的`mod.json`文件, 那么该文件夹就判定为不存在模组. 

目前NML不支持在子文件夹下搜索`mod.json`, 如果是用于声明模组请直接放置在模组文件夹下. 额外的key并不会与NCMS冲突.

[mod.json示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/mod.json)

# 解析

mod.json文件会按JSON格式等价解析成

```csharp
public class ModDeclare
{
    public string name;                      // 模组名
    public string author;                    // 作者名
    public string version;                   // 版本
    public string description;               // 描述
    public string iconPath;                  // 图标路径(相对于mod.json所在文件夹)
    public string RepoUrl;                   // 仓库地址
    public string[] Dependencies;            // 硬依赖
    public string[] OptionalDependencies;    // 软依赖
    public string[] IncompatibleWith;        // 不兼容模组列表(未实现)
}
```

其中, 模组名和作者名尽量不要包含特殊符号



在运行时, 会使用"作者名\_模组名"并取大写作为模组的`ID`, 其中属于ASCII码但不是数字或字母的字符会被替换为下划线. 如

<table><thead><tr><th width="172">作者名</th><th width="186">模组名</th><th>ID</th></tr></thead><tbody><tr><td>Nikon#7777</td><td>Example Mod</td><td>NIKON_7777_EXAMPLE_MOD</td></tr><tr><td>一米</td><td>中文名</td><td>一米_中文名</td></tr></tbody></table>


## 仓库地址

可以不填, 一般用于反馈bug或建议. 在模组列表中通过一个按钮访问(不知道怎么描述, 懂得都懂).


## 硬依赖

应当是模组ID的数组. 当所有硬依赖的模组均编译成功时, 该模组才会编译加载.



## 软依赖

应当是模组ID的数组. 其中的某个模组编译成功后, 该模组在编译时会加入编译成功的软依赖模组的ID作为宏(预定义常数)



## 不兼容模组列表

应当是模组ID的数组. 其功能未实现



## 图标路径

相对于模组文件夹, 可以为空, 为空时, 图标默认为NML的图标


# 访问

当一个模组能够访问到`ModDeclare`时, `ModDeclare`已经经过NML处理, 具体的定义如下

```csharp
public class ModDeclare
{
    // 模组名
    [JsonProperty("name")] 
    public string Name { get; private set; }
    // 模组ID
    public string UID { get; private set; }
    // 作者
    [JsonProperty("author")] 
    public string Author { get; private set; }
    // 版本
    [JsonProperty("version")] 
    public string Version { get; private set; }
    // 描述
    [JsonProperty("description")] 
    public string Description { get; private set; }
    // 仓库地址
    [JsonProperty("RepoUrl")] 
    public string RepoUrl { get; private set; }
    // 硬依赖模组ID数组
    [JsonProperty("Dependencies")] 
    public string[] Dependencies { get; private set; }
    // 软依赖模组ID数组
    [JsonProperty("OptionalDependencies")] 
    public string[] OptionalDependencies { get; private set; }
    // 不兼容模组ID数组
    [JsonProperty("IncompatibleWith")] 
    public string[] IncompatibleWith { get; private set; }
    // mod.json所在文件夹路径
    public string FolderPath { get; private set; } = null!;
    // 图标路径(相对于mod.json所在文件夹)
    [JsonProperty("iconPath")] 
    public string IconPath { get; private set; }
}
```
其中`JsonProperty`特性中的字符串表示解析时对应的key
