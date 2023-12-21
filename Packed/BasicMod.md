基础模组指的是 `BasicMod`

# 模组加载

与`IMod`略有不同, 在`BasicMod`中实现了`IMod`的`OnLoad`, 调用`OnModLoad`来初始化模组.

# 多语言文本

`BasicMod`提供了自动加载`Locales`文件夹下的语言文件. `cz.json`是简体中文, `en.json`是英文, `ch.json`是繁体中文.

下面是一个例子
```jsonc
// cz.json
{
    "Humans": "人类",
    "Orcs": "兽人"
}
```

除了`.json`文件外, 你也可以使用`.csv`文件来表示语言文件.

下面是一个例子`lang.csv`
```csv
key,cz,en,ch
Humans,人类,Humans,人類
Orcs,兽人,Orcs,獸人
```

# 模组设置

`BasicMod`设定了默认模组设置文件(模组文件夹下`default_config.json`文件)与恒久保存的模组设置文件.

`default_config.json`写法见[模组设置](../BasicConcept/ModConfiguration.md)

## 默认模组设置文件

给出了模组设置的格式

### 当默认模组设置添加/修改设置项(不包括项默认值)

恒久模组设置也会添加对应的设置项, 值为默认值

### 当默认模组设置删除设置项

恒久模组设置也会删除对应的设置项.