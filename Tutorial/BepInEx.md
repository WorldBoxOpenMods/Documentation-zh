# 介绍

NML本身不加载BepInEx模组，一切交由BepInEx本身处理，NML提供:
1. 识别并提供上传BepInEx模组
2. 将创意工坊订阅的BepInEx模组链接到本地的BepInEx文件夹
3. 自动安装BepInEx(从github下载，国内很可能失败)，当BepInEx不存在时

因此并不提供BepInEx模组的制作教程，仅提供相关规范。

为了让NML能够完整正确地识别BepInEx模组, 需要遵守以下约定:

1. `AssemblyTitleAttribute`标注模组名
2. `AssemblyCompanyAttribute`标注模组作者名
3. `AssemblyVersionAttribute`标注模组版本
4. `AssemblyDescriptionAttribute`标注模组简介

除此之外，文件夹结构需要满足如下

```
BepInEx
    |---plugins
    |       |---模组文件夹
    |       |       |---唯一主DLL文件
    |       |       |---icon.png(作为模组图标)
    |       |       |---其他非DLL文件
    |       |       |---其他文件夹
```

最后，只有引用了`Assembly-CSharp.dll`的DLL文件才会被认定为模组，否则为一般的BepInEx插件（跳过识别）