# 介绍

原版的`ItemAsset`同时表示了 武器, 防具, 饰品, 武器材料, 防具材料, 饰品材料, 装备词条 七个内容.

而实际上这七者并不应该完全被统合到一个类, Maxim 仍然这么做了, 导致`ItemAsset`在不同的位置其字段会有不同的使用情况. 

相关内容较为繁杂, 对于每个人如果都要研究明白是对模组制作者时间的极大浪费. 

因此NML提供了相关的装备创建器`NeoModLoader.General.Game.ItemAssetCreator`. 里面的创建函数的参数即为对应`ItemAsset`有用的所有字段.

# 武器材料

使用`CreateWeaponMaterial`创建`ItemAsset`后需要自行加入到`AssetManager.items_material_weapon`.

`CreateWeaponMaterial`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器材料的id|应当唯一|√|
|base_stats|BaseStats|属性加成||×|
|cost_gold|int|构建该材料消耗黄金的数量||×|
|cost_resources|KeyValuePair<string, int>[]|构建该材料消耗的<br>资源-数量的键值对数组|只有前面<br>最多2个元素有效|×|
|equipment_value|int|装备评估价值加成||×|
|metallic|bool|是否为金属材料|决定攻击/受击声音|×|
|minimum_city<br>_storage\_<br>resource_1|int|城市拥有第一种资源<br>的最低数量||×|
|mod_rank|int|在这里用于加成<br>装备评估价值<br>五倍数值加成||×|
|quality|ItemQuality|武器品质的最小值||×|
|tech_needed|string|打造该武器需要的<br>科技id||×|

# 饰品/防具材料

使用`CreateAccessoryOrArmorMaterial`创建`ItemAsset`后需要自行加入到`AssetManager.items_material_accessory`或`AssetManager.items_material_armor`.

`CreateAccessoryOrArmorMaterial`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器材料的id|应当唯一|√|
|base_stats|BaseStats|属性加成||×|
|cost_gold|int|构建该材料消耗黄金的数量||×|
|cost_resources|KeyValuePair<string, int>[]|构建该材料消耗的<br>资源-数量的键值对数组|只有前面<br>最多2个元素有效|×|
|equipment_value|int|装备评估价值加成||×|
|minimum_city<br>_storage\_<br>resource_1|int|城市拥有第一种资源<br>的最低数量||×|
|mod_rank|int|在这里用于加成<br>装备评估价值<br>五倍数值加成||×|
|quality|ItemQuality|武器品质的最小值||×|
|tech_needed|string|打造该武器需要的<br>科技id||×|

# 近战武器

# 远程武器

# 饰品/防具

# 装备词条