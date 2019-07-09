# Nyaa Docs
此处收集 NyaaCat 团队所开发的各种工具的文档。尽量使用中文撰写，力求表达到位易于理解。建议同时撰写英文版本以方便海外玩家浏览查阅。
# 活跃项目一览
- [核心][LanguageUtils](https://github.com/NyaaCat/LanguageUtils)
用于服务器端的本地化库，上游 [MascusJeoraly/LanguageUtils](https://github.com/MascusJeoraly/LanguageUtils) 似已不再维护，故继续开发。
- [核心][NyaaCore](https://github.com/NyaaCat/NyaaCore)
核心开发工具库。依赖 NMS，`VaultAPI`，`Essentials`，`LanguageUtils`。
- [核心][NyaaUtils](https://github.com/NyaaCat/NyaaUtils)
提供大量小工具和游戏机制。依赖 `WorldEdit`，`Essentials`，`NyaaCore`，`LangUtils`。可选依赖 `LockettePro`，`HamsterEcoHelper`。
- [经济][PlayTimeTracker](https://github.com/NyaaCat/PlayTimeTracker) 根据玩家在线时间给予奖励或惩罚。可选依赖 `Essentials`。
- [经济][NyaaPlayerCoser](https://github.com/NyaaCat/NyaaPlayerCoser) 类似 [Shopkeepers](https://dev.bukkit.org/projects/shopkeepers) 的 NPC 交易插件。依赖 NMS，`NyaaCore`，`ProtocolLib`。可选依赖 `HamsterEcoHelper`。
- [经济][HamsterEcoHelper](https://github.com/NyaaCat/HamsterEcoHelper) 天喵商城。提供牌子商店/世界商店/拍卖收购等服务。依赖 `Vault`，`NyaaCore`，`LangUtils`。可选依赖 `Essentials`，`LockettePro`。
- [经济][NyaaBank](https://github.com/NyaaCat/NyaaBank) 银行插件，允许玩家存款/借贷/收取存款利息等。依赖`Vault`，`NyaaUtils`。
- [经济][CapCat](https://github.com/NyaaCat/capcat) 资本化插件。依赖 `NyaaCore`。可选依赖 `HamsterEcoHelper`。
- [经济][IXP](https://github.com/NyaaCat/IXP) Item eXchange Portal 跨服物品传送。依赖 `NyaaCore`，`Vault`。
- [经济][Saika](https://github.com/NyaaCat/Saika)
- [管理][Yasui](https://github.com/NyaaCat/Yasui) 服务器性能提升插件。依赖 `NyaaCore`。可选依赖 `NyaaUtils`。[扩展阅读](https://blog.phoenixlzx.com/2017/05/05/reduce-minecraft-server-lag-without-limit-mob-amount/)
- [管理][LockettePro](https://github.com/NyaaCat/LockettePro) 锁箱插件。上游 [connection-lost/LockettePro](https://github.com/connection-lost/LockettePro) 似乎停更。可选依赖 `Vault`，`WorldGuard`，`ProtocolLib`，`CoreProtect`。
- [管理][Ourtown](https://github.com/NyaaCat/Ourtown) 城镇区划。依赖 `NyaaCore`，`Essentials`。可选依赖 `HamsterEcoHelper`。
- [管理][FrostKiller](https://github.com/NyaaCat/FrostKiller)
- [战斗][DeathChest](https://github.com/NyaaCat/DeathChest) 死亡箱子。依赖 `NyaaCore`。
- [战斗][RPGItems-Reloaded](https://github.com/NyaaCat/RPGItems-reloaded) 依赖 `NyaaCore`，`LangUtils`。可选依赖 `WorldGuard`。
- [战斗][InfiniteInfernal](https://github.com/NyaaCat/InfiniteInfernal)
- [战斗][Bloodmoon](https://github.com/NyaaCat/Bloodmoon) *血月升起之时……* 依赖 `NyaaCore`，`NyaaUtils`，`InfernalMobs`。可选依赖 `CoreProtect`，`FastAsyncWorldEdit`。
- [BC][buc](https://github.com/NyaaCat/buc)

# 其他项目
- [WIP][WorldLink](https://github.com/NyaaCat/WorldLink)
- [WIP][GenericTools](https://github.com/NyaaCat/GenericTools)
- [WIP][Tracit](https://github.com/NyaaCat/Tracit)
- [扩展]RedisProvider
- [扩展]rpgitems-ext-nyaacat
- [扩展]NyaaCoreTester
- [CI]NyaaCentral
- [CI]NyaaUtilsLangChecker
- [文档]NyaaDocs
- [网页]NyaaStats
- [网页]homepage
- [已停止]ce (CustomEnchantments)
- [已停止]Turrets
- [已停止]Lift
- [已停止][战斗][InfernalMobs](https://github.com/NyaaCat/InfernalMobs) 拥有强力技能的敌对生物。上游 [Eliminator/infernalmobs](https://bitbucket.org/Eliminator/infernalmobs/)。依赖 `NyaaCore`。可选依赖 `Vault`。

# 开发环境搭建
由于插件依赖复杂，为方便在开发环境对多个插件进行调试修改，建议使用`Gradle`的子项目功能。在一个空目录中执行以下命令，可以一次性批量克隆所有项目。

```setup.sh
#!/bin/bash

# gitclone <repo_name> [branch]
gitclone() {
    git clone "git@github.com:NyaaCat/$1.git"
    echo "include '$1'" >> settings.gradle
    if [ "$2" != "" ]; then
        pushd "$1"
        git checkout "$2"
        popd
    fi
}

gitclone LanguageUtils 1.14
gitclone NyaaCore 1.14
gitclone LockettePro
gitclone NyaaUtils 1.14
gitclone HamsterEcoHelper
gitclone NyaaBank
gitclone CapCat
gitclone Ourtown
gitclone Yasui
gitclone IXP
gitclone NyaaPlayerCoser
gitclone PlayTimeTracker

echo 'gradle.ext { useLocalDependencies = true }' >> settings.gradle
echo 'org.gradle.daemon=false' > gradle.properties
gradle wrapper --gradle-version 5.4.1
```

然后在`IntellijIDEA`中导入(Import)`settings.gradle`文件即可。建议选择“using explicit module groups”，并取消选择“create seperate module per source set”。所有项目都会自动依赖本地代码而不是CI仓库。如果你没有对仓库的写权限，你需要手动替换为HTTPS的仓库地址。目前只有部分项目支持这种依赖配置，其他项目在完成迁移后会添加到这个列表中。

由于CI仍然使用maven仓库作为编译依赖，为避免CI失败，请务必先上传(git push)被依赖的项目的变动，再上传下游项目的变动。

