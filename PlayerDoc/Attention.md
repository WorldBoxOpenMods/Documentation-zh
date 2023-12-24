# 当模组内容不更新时

有多种原因:
1. Steam抽风了, 没自动下载
2. 本地Mods文件夹中存在相同id的模组(优先加载本地, 重复id的模组不加载)
3. NML可能出问题了, 反馈bug, 一般解决方法: 尝试手动更新NML, 并删除`游戏路径/worldbox_Data/StreamingAssets/mods/NML`文件夹

# 与NCMS共存时

1. 不推荐与NCMS共同安装, 因为NML支持几乎所有NCMS模组
2. 当与NCMS共存时, NML会放弃加载本地Mods文件夹下的模组, 仅加载创意工坊目录下的模组

# 当自动更新失败时

重新下载新的NML本体, 按照[安装教程](./Install.md)重新覆盖安装即可