# GTFO-Player-Movement-and-Health

移动与生命。本仓包含以下MOD／共享组件，各自维护文件放在自己的目录。

[定位入口](#modules) · [依赖与联动](#relations) · [开发与排查](#development) · [来源说明](#sources)

<a id="modules"></a>
## 定位入口

| 功能／组件 | 版本 | 修改位置与输入 | 维护方式 | 测试材料 |
| --- | --- | --- | --- | --- |
| 移动、滑铲与体力 `PrisonerMovementCustom` | 1.0.2 | [PrisonerMovementCustom/baseline](PrisonerMovementCustom/baseline) | 冻结DLL＋身份迁移 | 无独立源码测试入口 |
| 生命调整 `PrisonerHealthCustom` | 1.0.1 | [PrisonerHealthCustom/baseline](PrisonerHealthCustom/baseline) | 冻结DLL＋身份迁移 | 无独立源码测试入口 |

具体路径、版本、GUID、资源和依赖的机器登记见[repo.json](repo.json)。src是实现，tests是测试；IntegrationTests用于跨MOD场景或调度配方，Shared仅保存真正共享的接口。

普通玩家从[Releases](https://github.com/PreLuna/GTFO-Player-Movement-and-Health/releases)下载已经构建的安装ZIP，按对应版本说明安装并准备前置；不需要构建工具仓。退出游戏后将ZIP中的BepInEx合并到已配置前置的游戏目录，替换同功能旧版以免重复加载；个人CFG不包含在安装包中。GitHub的Source code／Code ZIP用于开发，不能把baseline原件直接当安装DLL。

<a id="relations"></a>
## 依赖与联动

移动与生命属于同一维护域，两插件互无硬依赖，可以分别安装。二者当前均以冻结DLL加身份迁移构建，完整主体源码尚未恢复。

| 模块 | 插件硬前置／声明版本 | 可选联动／软依赖 |
| --- | --- | --- |
| PrisonerMovementCustom | 无插件硬前置声明 | 无插件软依赖声明 |
| PrisonerHealthCustom | 无插件硬前置声明 | 无插件软依赖声明 |

所有插件仍需GTFO及相应BepInEx IL2CPP环境。版本保留加载器原始声明表达式；编译引用、运行硬前置和可选桥分别判断。

<a id="development"></a>
## 开发与排查

| 要修改／排查的功能 | 先读哪里 | 联动范围 |
| --- | --- | --- |
| 移动／生命行为修改 | [PrisonerMovementCustom/baseline](PrisonerMovementCustom/baseline) | 基线是输入而非可直接编辑源码；应先恢复并验证相关历史补丁链，生命基线在PrisonerHealthCustom/baseline。 |

冻结baseline保留原始WangLocal文件名、内部身份和SHA256，构建后输出PreLuna版；它不是完整主体源码。行为调整须先证明补丁输入链，不能只改DLL文件名。维护者本地历史冷档不随本仓提供，未据此宣称源码已经恢复。

开发环境：支持C#12编译的PowerShell 7、.NET 6 runtime、GTFO/BepInEx的core与生成的interop。将[共用工具仓](https://github.com/PreLuna/GTFO-Mod-Build-and-Verification-Tools)放在本仓旁边，可通过BuildToolsRoot覆盖位置。

先审查并登记输入／维护锁，再在本仓目录执行（路径换成本机实际值，重复构建前显式清理本仓忽略的out）：

```powershell
./Build.ps1 -GameRoot 'D:/Games/GTFO' -RuntimeRoot 'C:/Program Files/dotnet/shared/Microsoft.NETCore.App/6.0.16'
```

本仓没有Test.ps1，也不宣称独立源码回归通过；Build负责冻结输入的身份迁移与程序集核验。修改相关历史补丁后需单独建立测试和游戏内验收。

构建与离线测试不安装到游戏。`.cs`是功能／测试／辅助源码，`.ps1`是维护脚本，编译所得`.dll`才供游戏加载；运行CFG不加入源码仓。

维护锁与提交步骤见[共用维护流程](https://github.com/PreLuna/GTFO-Mod-Build-and-Verification-Tools#maintenance)，打包要求见[发布与打包](https://github.com/PreLuna/GTFO-Mod-Build-and-Verification-Tools#packaging)。仅使用Releases的玩家不需要这些开发步骤。

<a id="sources"></a>
## 来源说明

- PrisonerMovementCustom：APEX_Prisoners；作者 Localia；来源版本 原始输入快照manifest标注3.0.1；独立分支当前1.0.2，不跟随原包升级。
- PrisonerHealthCustom：GTFO.EZ；作者 MindAttic；来源版本 工作区原包标注1.0.0；当前输入已经过定制。

保留源文件中的作者与版权声明。部分模组包含第三方派生实现或冻结基线，本说明不替代上游许可证，也不新增再分发授权；本仓库没有统一重授权声明。
