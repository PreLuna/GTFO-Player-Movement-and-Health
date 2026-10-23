# GTFO-Player-Movement-and-Health

移动与生命。各MOD的维护文件直接放在自己的目录内。

| MOD／目录 | 版本 | 维护方式 | 必要前置／声明版本 | 可选联动／软依赖 |
| --- | --- | --- | --- | --- |
| [移动、滑铲与体力](PrisonerMovementCustom/) | 1.0.2 | 冻结DLL＋身份迁移 | 无插件硬前置声明 | 无插件软依赖声明 |
| [生命调整](PrisonerHealthCustom/) | 1.0.1 | 冻结DLL＋身份迁移 | 无插件硬前置声明 | 无插件软依赖声明 |

所有插件均需GTFO与相应BepInEx IL2CPP环境。无插件硬依赖声明不表示可脱离游戏运行；软依赖也可能对应某项功能的启用条件。版本列保留加载器声明表达式。

## MOD之间的关系

PrisonerMovementCustom与PrisonerHealthCustom按玩家行为主题共同维护，彼此没有插件硬依赖声明，可以分别维护与安装。两者当前都以冻结DLL为输入，历史补丁尚未恢复为当前可重建流水线。

## 下载与安装

普通玩家从 [Releases](https://github.com/PreLuna/GTFO-Player-Movement-and-Health/releases) 下载安装ZIP，退出游戏后将BepInEx合并到已配置前置的游戏目录，替换同功能旧版以免重复加载。个人配置不包含在安装包中。Source code ZIP用于开发。已发布标签固定对应原提交；本地目录整理不覆盖旧安装包。

构建、测试及修改入口见 [DEVELOPMENT.md](DEVELOPMENT.md)，来源见 [NOTICE.md](NOTICE.md)，机器可读路径和依赖见 [repo.json](repo.json)。
