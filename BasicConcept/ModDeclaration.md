# 模组声明

这一节介绍`mod.json`可用的配置

mod.json文件会按JSON格式等价解析成

```csharp
public class ModDeclare
{
    public string name;                      // 模组名
    public string author;                    // 作者名
    public string version;                   // 版本
    public string description;               // 描述
    public string iconPath;                  // 图标路径(相对于模组文件夹)
    public string RepoUrl;                   // 仓库地址
    public string[] Dependencies;            // 硬依赖
    public string[] OptionalDependencies;    // 软依赖
    public string[] IncompatibleWith;        // 不兼容模组列表(未实现)
}
```

其中, 模组名和作者名尽量不要包含特殊符号



在运行时, 会使用"作者名\_模组名"并取大写作为模组的`ID`, 其中属于ASCII码但不是数字或字母的字符会被替换为下划线. 如

<table><thead><tr><th width="172">作者名</th><th width="186">模组名</th><th>ID</th></tr></thead><tbody><tr><td>Nikon#7777</td><td>Example Mod</td><td>NIKON_7777_EXAMPLE_MOD</td></tr><tr><td>一米</td><td>中文名</td><td>一米_中文名</td></tr></tbody></table>



## 硬依赖

应当是模组ID的数组. 当所有硬依赖的模组均编译成功时, 该模组才会编译加载.



## 软依赖

应当是模组ID的数组. 其中的某个模组编译成功后, 该模组在编译时会加入编译成功的软依赖模组的ID作为宏(预定义常数)



## 不兼容模组列表

应当是模组ID的数组. 其功能未实现



## 图标路径

相对于模组文件夹, 可以为空, 为空时, 图标默认为NML的图标
