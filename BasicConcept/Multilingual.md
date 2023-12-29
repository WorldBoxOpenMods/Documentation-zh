# 介绍

NML为模组提供了多语言文本的支持, 支持能够在游戏内顺利切换语言.

[csv类型示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/Locales/items_lang.csv)

[json类型示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/Locales/cz.json)

[手动加载示例](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L62)大约在62行左右, `Reload`函数中, 自行寻找

# 使用

NML在语言文本的支持集中在`NeoModLoader.General.LM`

你可以用`LM.Get`来获取一个key在当前语言情况下对应的文本.

`LM.LoadLocales`用于读取`.csv`类型的文本文件来加载语言文本

`LM.LoadLocale`用于读取`.json`类型的文本文件来加载语言文本

`LM.AddToCurrentLocale`用于将语言文本动态加载

`LM.Add`用于将语言文本动态加载给对应的语言

`LM.ApplyLocale`用于将加载语言文本的更改应用到所有`LocalizedText`

## csv类型的文本文件

下面是一个例子`lang.csv`
```csv
key,cz,en,ch
Humans,人类,Humans,人類
Orcs,兽人,Orcs,獸人
```

## json类型的文本文件

下面是一个例子
```jsonc
// cz.json
{
    "Humans": "人类",
    "Orcs": "兽人"
}
```

# 自动加载

你的模组主类需要实现`ILocalizable`接口, 在`GetLocaleFilesDirectory`返回语言文本文件夹的路径(真实文件系统). 在语言文本文件夹下的`.csv`会被加载, `.json`文件会被加载为其无后缀文件名的语言文本(如`cz.json`会给代码为`cz`的语言加载语言文本)