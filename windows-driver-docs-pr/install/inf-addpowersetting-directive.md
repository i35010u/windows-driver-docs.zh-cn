---
title: INF AddPowerSetting 指令
description: AddPowerSetting 指令引用用于修改或创建电源设置信息的一个或多个部分。
ms.assetid: 0231ba90-5de4-4f5a-83bb-0f73be4b23ae
keywords:
- INF AddPowerSetting 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddPowerSetting Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7285dcf05973b87c886ce0a9db0a90d65f0d421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532974"
---
# <a name="inf-addpowersetting-directive"></a>INF AddPowerSetting 指令


**AddPowerSetting**指令引用用于修改或创建电源设置信息的一个或多个部分。 每个*添加电源设置部分*定义的电源设置的允许的值为电源设置、 电源设置的友好名称并将电源设置的说明。 *添加电源设置部分*还指定了每个电源方案个性的默认值。 有关电源设置和电源方案个性的详细信息，请参阅[管理设备性能状态](https://msdn.microsoft.com/library/windows/hardware/ff554353)。

```ini
[DDInstall] | 
[DDInstall.HW] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows Vista)
[ClassInstall32.ntamd64]  (Windows Vista)
[ClassInstall32.ntarm] 
[ClassInstall32.ntarm64]  



AddPowerSetting=add-power-setting-section[,add-power-setting-section]
```

一般情况下，*添加电源设置部分*包括以下指令：

-   一个**子组**指令。
-   一个**设置**指令
-   两个或多个列表**值**指令或一个**ValueRange**指令。
-   一组六篇文章构成**默认**指令。

*添加电源设置部分*采用以下两个可能的形式之一：

-   如果允许的电源设置数值最可定义为一组两个或多个离散值，使用一系列**值**指令来指定允许的值，如下所示：

    ```ini
    [add-power-setting-section]

    [SubGroup = {subgroup-guid}] | SubGroup = {subgroup-guid}, subgroup-name, subgroup-description, subgroup-icon
    Setting = {setting-guid}, [setting-name],[setting-description],[setting-icon]
    Value = value-index, value-name,[value-description], value-flags, value-data 
    Value = value-index, value-name,[value-description], value-flags, value-data
    [Value = value-index, value-name,[value-description], value-flags, value-data
    ...
    Value = value-index, value-name,[value-description], value-flags, value-data]

    (Six required Default directives, each one of which has the following form)
    Default = power-scheme-personality-GUID, AC/DC-index, default-setting-index | default-setting-value 
    ...
    ```

-   如果允许的电源设置值可以最好地定义为指定范围内的非负整数值的递增序列中，使用一个**ValueRange**指令，用于指定允许的值，如下所示：

    ```ini
    [add-power-setting-section]

    [SubGroup = {subgroup-guid}] | 
    SubGroup = {subgroup-guid}, subgroup-name, subgroup-description, subgroup-icon
    Setting = {setting-guid}, [setting-name],[setting-description],[setting-icon]
    ValueRange = range-minimum-value, range-maximum-value, range-increment, [range-unit-label] 

    (Six required Default directives, each one of which has the following form)
    Default = power-scheme-personality-GUID, AC/DC-index, default-setting-index | default-setting-value 
    ...
    ```

## <a name="entries"></a>条目


**请注意**  除*值数据*条目，提供一个字符串值的所有以下项可以在中指定字符串中所述的方法之一[指定 AddPowerSetting字符串输入值](#specifying-an-addpowersetting-string-entry-value)。

 

<a href="" id="subgroup"></a>**SubGroup**  
子组分组逻辑上相关的电源设置。

若要指定系统定义的子组，包括**子组**指令并仅提供*子组 guid*条目。 系统定义子组由常量 GUID_*Xxx*_SUBGROUP 和 NO_SUBGROUP_GUID 中, 定义*wdm.h 中*。

例如，GUID_VIDEO_SUBGROUP 表示包含电源方案个性的视频的电源设置的子组。 NO_SUBGROUP_GUID 常量表示逻辑上不属于任何子组的设置的集合。 如果**子组**不包括指令，则该设置是默认情况下添加到逻辑上不属于任何子组的设置的集合。

若要定义新的子组，包括**子组**指令，并提供所需的以下条目：*子组 guid*，*子组名称*， *子组说明*，和*子组图标。* 必须是唯一的新的子组的 GUID 和其他项应为尽可能具有描述性。

<a href="" id="subgroup-guid"></a>*subgroup-guid*  
所需的条目提供标识子组的 GUID。 此条目的格式是 **{**<em>XXXXXXXX XXXX XXXX XXXXXXXXXXXX</em>**}**，其中"X"是一个十六进制数字。

例如，系统定义的常量 GUID_VIDEO_SUBGROUP 的值是 {7516B95F-F776-4464-8C53-06167F40CC99}。 此 GUID 表示包含电源方案个性的视频的电源设置的子组。

<a href="" id="subgroup-name"></a>*subgroup-name*  
一个字符串，指定电源设置的子组名称。 如果该子组为系统定义的子组，不应提供此项。 如果是新的子组，则需要此项。

<a href="" id="subgroup-description"></a>*subgroup-description*  
一个字符串，描述用户到 power 子组。 如果该子组为系统定义的子组，不应提供此项。 如果是新的子组，则需要此项。

<a href="" id="subgroup-icon"></a>*subgroup-icon*  
对一个图标资源的引用。 如果该子组为系统定义的子组，不应提供此项。 如果是新的子组，则需要此项。

必须为非特定于语言的注册表值指定一个图标资源。 有关如何指定一个非特定于语言的注册表值的信息，请参阅[指定 AddPowerSetting 字符串条目值](#specifying-an-addpowersetting-string-entry-value)。

<a href="" id="setting"></a>**设置**  
**设置**指令标识的设置部分中的其他条目应用到所有。 一个**设置**指令需要在添加电源设置部分和只能有一个**设置**指令中添加的电源设置部分。 如果 INF 文件定义了多个设置，则必须自己添加电源设置节中定义的每个设置。

以下是与之关联的条目**设置**指令。

<a href="" id="setting-guid"></a>*setting-guid*  
指定表示将电源设置 GUID 的必需的项。 此条目的格式是 **{**<em>XXXXXXXX XXXX XXXX XXXXXXXXXXXX</em>**}**，其中每个"X"是一个十六进制数字。

例如，以下是自定义的 GUID 值: {BFC0D9E9-549C-483D-AD2A-3D90C98A8B03}。

<a href="" id="setting-name"></a>*setting-name*  
指定包含将电源设置的友好名称的字符串的可选项。 **电源选项**控件面板中向用户显示此友好名称。

<a href="" id="setting-description"></a>*setting-description*  
指定电源设置以及设置对系统电源和性能的影响，向用户描述的字符串的可选项。

<a href="" id="setting-icon"></a>*setting-icon*  
可选条目，是对一个图标资源的引用。 必须按非特定于语言的注册表值指定一个图标资源。

有关如何指定的语言特定注册表值的信息，请参阅[指定 AddPowerSetting 字符串条目值](#specifying-an-addpowersetting-string-entry-value)。

<a href="" id="value"></a>**值**  
一个**值**指令定义允许使用的电源设置的值。 **值**指令应在值最可定义为一组两个或多个值，其中每个值可以具有值特定于自定义数据类型。 在此情况下，添加-power-设置-部分应包含两个或多个**值**指令。 用户可以选择在下列值之一**电源选项**控制面板配置电源方案中。

如果允许的电源设置值最适合所述为递增组的非负整数的范围内，使用**ValueRange**指令而不是**值**指令，用于指定所允许电源设置值。

<a href="" id="value-index"></a>*value-index*  
指定一个唯一索引值，即大于或等于零，并用于引用相应的值设置所需的项。 **电源选项**控制面板中显示电源设置值到其相应的索引值的顺序中的用户从最低最高。

<a href="" id="value-name"></a>*value-name*  
提供了一个字符串的所需的项，提供了相应的设置值的友好名称。 **电源选项**控件面板中向用户显示的电源设置值的友好名称。

<a href="" id="value-description"></a>*value-description*  
可选条目，用于提供电源设置值以及设置值对系统电源和性能的影响，向用户描述的字符串。

<a href="" id="value-flags"></a>*value-flags*  
值数据的相应项的数据类型指定为下表中所指示所需的项。

| 标记值 | 数据类型   |
|------------|-------------|
| 0x00000001 | [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) |
| 0x00010001 | [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)  |
| 0x00000000 | [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)     |

 

<a href="" id="value-data"></a>*value-data*  
提供相应的设置值的数据所需的条目，其中的格式取决于指定的相对应的数据类型*值标志*条目，如下所示：

-   一个[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值可以通过使用 0 x 表示法，或作为以逗号分隔的列表，而无需 0 x 表示法的配对十六进制数字的指定以十六进制格式。

    例如，以下项是等效的：0xFEDCBA9876543210 和以下配对的十六进制数字的以逗号分隔列表：FE、 DC、 BA 98、 76、 54、 32、 10。

-   一个[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值可以以十六进制格式 （通过使用 0 x 表示法） 或在指定的十进制格式。
-   一个[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值仅表示作为字符串括在双引号 ("*带引号的字符串*") 或作为 %*strkey*INF中定义的%令牌[**字符串**](inf-strings-section.md) INF 文件的节。

**请注意**  您不应使用字符串值，因为它们不能进行本地化。 请改用类型的值[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)或[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

 

<a href="" id="valuerange"></a>**ValueRange**  
使用**ValueRange**指令如果最佳允许的电源设置值定义为指定范围内的非负整数值的递增序列。 电源管理器验证在用户选择的设置**电源选项**控制面板中是其中一种允许的值。 确定允许的值集的最小允许值，最多允许值和允许的范围内的值之间的增量。 如果它满足以下，允许值：

```ini
range-minimum-value + k*range-increment
```

其中*范围最小值*大于或等于零， *k*并*范围增量*应大于或等于一和的值是小于或等于*范围最大值*。 此外，*范围最大值*应该等于*范围最小值* + *k*\**范围递增*某些 k。

例如，对于*范围最小值*等于 0，*范围最大值*等于 10，和一个*范围增量*等于 2，允许的值如下所示：0、 2、 4、 6、 8 和 10。

如果允许的电源设置值可最佳描述为一系列值，其中每个值可以具有值特定于自定义数据类型，使用**值**指令而不是**ValueRange**指令。

<a href="" id="range-minimum-value"></a>*range-minimum-value*  
类型的值[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)指定最小允许的电源设置。

<a href="" id="range-maximum-value"></a>*range-maximum-value*  
类型的值[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) ，指定的最大允许的电源设置值。 最大值必须大于或等于最小值和应等于最小值的范围值 + *k\*范围增量*，对于某些整数*k*大于零。

<a href="" id="range-increment-"></a>*range-increment*   
类型的值[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)大于零。 此值指定在由指定的非独占范围内的连续值之间的差异*范围最小值*并*范围最大值*。

<a href="" id="range-unit-label-"></a>*range-unit-label*   
描述电源设置值的可选字符串。 一起使用的字符串*设置名称*，通知用户的数据类型的输入。

例如，该字符串可用于指定值的单位，例如"分钟数"或"%"（表示百分比）。

<a href="" id="default"></a>**默认值**  
有六**默认**必须包括在指令**AddPowerSetting**部分。 一个**默认**指令指定的默认值为一种适用于 AC 电源状态的三个系统定义的电源方案个性和适用于 DC 电源状态的三个系统定义的电源方案个性。

默认值为有效且准确至关重要。 如果用户未手动设置电源设置，电源管理器将使用指定的默认值**默认**指令。

<a href="" id="power-scheme-personality-guid"></a>*power-scheme-personality-GUID*  
一个标识此默认值适用于的电源方案的以下 Guid。

| 个性      | GUID                                   |
|------------------|----------------------------------------|
| “节能程序”      | {A1841308-3541-4FAB-BC81-F71556F20B4A} |
| 高性能 | {8C5E7FDA-E8BF-4A96-9A85-A6E23A8C635C} |
| 平衡         | {381B4222-F694-41F0-9685-FF5BB260DF2E} |

 

在中定义这些 Guid *wdm.h 中*。

<a href="" id="ac-dc-index"></a>*AC/DC-index*  
如果*AC/DC-索引*为 0，则该设置将应用到 AC 电源状态; 如果*AC/DC-索引*为 1，设置是适用于 DC 电源状态。 0 或 1 以外的值无效。

<a href="" id="default-setting-index-"></a>*default-setting-index*   
如果**值**指令用于指定允许的值，*默认设置索引*的值*value 索引条目*的**值**指令。 如果**ValueRange**指令用于指定允许的值，此条目将不适用于。

<a href="" id="default-setting-value-"></a>*default-setting-value*   
如果**ValueRange**指令用于指定允许的值，*默认设置值*是一个由指定的允许值**ValueRange**指令。 如果**值**指令用于指定允许的值，此条目将不适用于。

<a name="remarks"></a>备注
-------

*添加电源设置部分*名称必须唯一 INF 文件，但可以被多个**AddPowerSetting**指令相同的 INF 文件中。 每个节名必须遵循中所述的常规规则[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

卸载设备后，电源管理器不会自动删除设备电源策略。 通过在中定义的系统提供的电源设置例程的共同安装程序可执行安装或删除电源设置、 值和默认值*Powrprof.h*。 有关这些电源管理例程的详细信息，请参阅随 Microsoft Windows SDK 文档提供电源管理的参考。

此外， *Powercfg.exe*命令行工具可用于更改电源设置。 璝惠*Powercfg.exe*，请参阅 Microsoft 帮助和支持中心。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

### <a name="specifying-an-addpowersetting-string-entry-value"></a>指定为 AddPowerSetting 字符串条目的值

除*数值数据*类型的条目[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)，其他字符串条目的所有值都附有**AddPowerSetting**指令可以表示为字符串括在双引号 ("*带引号的字符串*")，作为 %*strkey*INF 字符串部分的 INF 文件，或作为非特定于语言的注册表值中定义的 %令牌。

非特定于语言的注册表值用于支持 Windows 多语言用户界面 (MUI)，并按如下所示指定：

```ini
"@file-path,-resourceID[;comment]"
```

指定非特定于语言的注册表值的条目如下所示：

<a href="" id="file-path"></a>*file-path*  
包含资源文件的完全限定的路径。

<a href="" id="resourceid"></a>*resourceID*  
相应的资源的资源 ID。 一个字符串，对于*resourceID*引用一个字符串。 在一个图标的情况下*resourceID*引用一个图标。

<a href="" id="comment"></a>*注释*  
一个可选值，可用于协助调试或提供有关设置的其他注释。 对于字符串资源，电源管理器不会组合或显示了指定的资源字符串的注释字符串。

有关如何指定非特定于语言的注册表值的详细信息，请参阅[呈现 Shell 和注册表字符串](https://go.microsoft.com/fwlink/p/?linkid=70407)。

<a name="examples"></a>示例
--------

以下两个示例定义控制的 LCD 亮度的电源设置。 第一个示例演示如何使用**值**指令来定义最小、 中和最大的 LCD 亮度值。

```ini
// Within a DDinstall or ClassInstall23 section
AddPowerSetting=LCDDim
...

[LCDDim]
SubGroup = {7516B95F-F776-4464-8C53-06167F40CC99}
Setting = {381B4222-F694-41F0-9685-FF5BB260DF2E}, "LCD Brightness", "Controls the brightness of the LCD display"

Value = 0, "Low", "Minimum Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x50
Value = 1, "Medium", "Medium Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x75
Value = 2, "High", "Maximum Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x100

Default = %GUID_MAX_POWER_SAVINGS%, %AC%, 0
Default = %GUID_MAX_POWER_SAVINGS%, %DC%, 0
Default = %GUID_TYPICAL_POWER_SAVINGS%, %AC%, 2
Default = %GUID_TYPICAL_POWER_SAVINGS%, %DC%, 1
Default = %GUID_MIN_POWER_SAVINGS%, %AC%, 2
Default = %GUID_MIN_POWER_SAVINGS%, %DC%, 2
...

[Strings]
GUID_MAX_POWER_SAVINGS = {a1841308-3541-4fab-bc81-f71556f20b4a}
GUID_TYPICAL_POWER_SAVINGS = {381b4222-f694-41f0-9685-ff5bb260df2e}
GUID_MIN_POWER_SAVINGS = {8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c}
AC = 0
DC = 1
FLG_ADDREG_TYPE_DWORD = 0x00010001
```

第二个示例演示如何使用**ValueRange**指令来定义一系列允许的 LCD 亮度值从 0%到 100%，增量为 1%之间允许的值而变化。

```ini
// Within a DDinstall or a ClassInstall23 section
AddPowerSetting=LCDDimRange
...

[LCDDimRange]
SubGroup = {7516B95F-F776-4464-8C53-06167F40CC99}
Setting = {381B4222-F694-41F0-9685-FF5BB260DF2E}, "LCD Brightness", "Controls the brightness of the LCD display"
ValueRange = 0, 100, 1, "%"
Default = %GUID_MAX_POWER_SAVINGS%, %AC%, 50
Default = %GUID_MAX_POWER_SAVINGS%, %DC%, 50
Default = %GUID_TYPICAL_POWER_SAVINGS%, %AC%, 95
Default = %GUID_TYPICAL_POWER_SAVINGS%, %DC%, 50
Default = %GUID_MIN_POWER_SAVINGS%, %AC%, 100
Default = %GUID_MIN_POWER_SAVINGS%, %DC%, 100

[Strings]
GUID_MAX_POWER_SAVINGS = {a1841308-3541-4fab-bc81-f71556f20b4a}
GUID_TYPICAL_POWER_SAVINGS = {381b4222-f694-41f0-9685-ff5bb260df2e}
GUID_MIN_POWER_SAVINGS = {8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c}
AC = 0
DC = 1
```

## <a name="see-also"></a>另请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

 

 






