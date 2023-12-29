# 介绍

原版的`ItemAsset`同时表示了 武器, 防具, 饰品, 武器材质, 防具材质, 饰品材质, 装备词条 七个内容.

而实际上这七者并不应该完全被统合到一个类, Maxim 仍然这么做了, 导致`ItemAsset`在不同的位置其字段会有不同的使用情况. 

相关内容较为繁杂, 对于每个人如果都要研究明白是对模组制作者时间的极大浪费. 

因此NML提供了相关的装备创建器`NeoModLoader.General.Game.ItemAssetCreator`. 里面的创建函数的参数即为对应`ItemAsset`有用的所有字段.

[相关示例代码](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleItems.cs)

# 武器材质

使用`CreateWeaponMaterial`创建`ItemAsset`后需要自行加入到`AssetManager.items_material_weapon`.

`CreateWeaponMaterial`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器材质的id|应当唯一|√|
|base_stats|BaseStats|属性加成|-|×|
|cost_gold|int|构建该材质消耗黄金的数量|-|×|
|cost_resources|KeyValuePair<string, int>[]|构建该材质消耗的<br>资源-数量的键值对数组|只有前面<br>最多2个元素有效|×|
|equipment_value|int|装备评估价值加成|-|×|
|metallic|bool|是否为金属材质|决定攻击/受击声音|×|
|minimum_city<br>_storage\_<br>resource_1|int|城市拥有第一种资源<br>的最低数量|-|×|
|mod_rank|int|在这里用于加成<br>装备评估价值<br>五倍数值加成|-|×|
|quality|ItemQuality|武器品质的最小值|-|×|
|tech_needed|string|打造该武器需要的<br>科技id|-|×|

# 饰品/防具材质

使用`CreateAccessoryOrArmorMaterial`创建`ItemAsset`后需要自行加入到`AssetManager.items_material_accessory`或`AssetManager.items_material_armor`.

`CreateAccessoryOrArmorMaterial`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器材质的id|应当唯一|√|
|base_stats|BaseStats|属性加成|-|×|
|cost_gold|int|构建该材质消耗黄金的数量|-|×|
|cost_resources|KeyValuePair<string, int>[]|构建该材质消耗的<br>资源-数量的键值对数组|只有前面<br>最多2个元素有效|×|
|equipment_value|int|装备评估价值加成|-|×|
|minimum_city<br>_storage\_<br>resource_1|int|城市拥有第一种资源<br>的最低数量|-|×|
|mod_rank|int|在这里用于加成<br>装备评估价值<br>五倍数值加成|-|×|
|quality|ItemQuality|武器品质的最小值|-|×|
|tech_needed|string|打造该武器需要的<br>科技id|-|×|

# 近战武器

使用`CreateMeleeWeapon`创建`ItemAsset`后会自动加入到`AssetManager.items`

`CreateMeleeWeapon`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器的id|应当唯一<br>与所有其他装备不同|√|
|base_stats|BaseStats|属性加成|-|×|
|materials|List<string>|可选的材质|从武器材质中选|×|
|item_modifiers|List<string>|自带的词条|是词条id的列表<br>不是词条type|×|
|name_class|string|装备类型名称|注意要自己添加<br>"name_class_装备可能的品质"<br>的翻译文本|×|
|name_templates|List<string>|传说品质可选命名模板|注意要自己添加<br>对应的命名器|×|
|tech_needed|string|所需科技|单个科技的id|×|
|action_attack_target|AttackAction|攻击目标时触发的Action|-|×|
|action_special_effect|WorldAction|持有时不断触发的Action|-|×|
|special_effect_interval|float|持有时不断触发的Action<br>的触发间隔|单位为秒|×|
|equipment_value|int|装备评估价值加成|-|×|
|path_slash_animation|string|攻击动画|-|×|

# 远程武器

使用`CreateRangeWeapon`创建`ItemAsset`后会自动加入到`AssetManager.items`

`CreateRangeWeapon`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|武器的id|应当唯一<br>与所有其他装备不同|√|
|projectile|string|投掷物的id|使用现成投掷物<br>或自己添加<br>对应投掷物|√|
|base_stats|BaseStats|属性加成|-|×|
|materials|List<string>|可选的材质|从武器材质中选|×|
|item_modifiers|List<string>|自带的词条|是词条id的列表<br>不是词条type|×|
|name_class|string|装备类型名称|注意要自己添加<br>"name_class_装备可能的品质"<br>的翻译文本|×|
|name_templates|List<string>|传说品质可选命名模板|注意要自己添加<br>对应的命名器|×|
|tech_needed|string|所需科技|单个科技的id|×|
|action_attack_target|AttackAction|攻击目标时触发的Action|-|×|
|action_special_effect|WorldAction|持有时不断触发的Action|-|×|
|special_effect_interval|float|持有时不断触发的Action<br>的触发间隔|单位为秒|×|
|equipment_value|int|装备评估价值加成|-|×|
|path_slash_animation|string|攻击动画|-|×|

# 饰品/防具

使用`CreateArmorOrAccessory`创建`ItemAsset`后会自动加入到`AssetManager.items`

`CreateArmorOrAccessory`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|装备的id|应当唯一<br>与所有其他装备不同|√|
|equipmentType|EquipmentType|饰品/防具类型|不能是武器|√|
|base_stats|BaseStats|属性加成|-|×|
|materials|List<string>|可选的材质|从武器材质中选|×|
|item_modifiers|List<string>|自带的词条|是词条id的列表<br>不是词条type|×|
|name_class|string|装备类型名称|注意要自己添加<br>"name_class_装备可能的品质"<br>的翻译文本|×|
|name_templates|List<string>|传说品质可选命名模板|注意要自己添加<br>对应的命名器|×|
|tech_needed|string|所需科技|单个科技的id|×|
|action_attack_target|AttackAction|攻击目标时触发的Action|-|×|
|action_special_effect|WorldAction|持有时不断触发的Action|-|×|
|special_effect_interval|float|持有时不断触发的Action<br>的触发间隔|单位为秒|×|
|equipment_value|int|装备评估价值加成|-|×|

# 装备词条

使用`CreateAndAddModifier`创建`ItemAsset`后会自动加入到`AssetManager.items_modifiers`并更新到对应的`pool`

`CreateAndAddModifier`参数如下

|参数名|类型|解释|备注|必需|
|:----:|:----:|:----:|:----:|:----:|
|id|string|词条的id|应当唯一<br>与所有其他词条不同|√|
|mod_type|string|词条的类型|用于判断是否为同类型词条<br>同类型词条才能比较等级|√|
|mod_rank|int|词条的等级|同样有5倍于数值的<br>装备评估价值加成|√|
|translation_key|string|词条的翻译key|需要自己添加对应的翻译文本|√|
|rarity|int|稀有度(常见度)|越大越常见<br>游戏本体的值大多集中于1或3|×|
|equipment_value|int|装备评估价值加成|-|×|
|quality|ItemQuality|武器品质的最小值|-|×|
|base_stats|BaseStats|属性加成|-|×|
|action_attack_target|AttackAction|攻击目标时触发的Action|-|×|
|action_special_effect|WorldAction|持有时不断触发的Action|-|×|
|special_effect_interval|float|持有时不断触发的Action<br>的触发间隔|单位为秒|×|