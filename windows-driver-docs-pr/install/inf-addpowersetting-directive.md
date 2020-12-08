---
title: INF AddPowerSetting 指令
description: AddPowerSetting 指令将引用一个或多个用于修改或创建电源设置信息的部分。
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
ms.openlocfilehash: 63d15ccdd6895174a621d76fb4eb68f4b29b73b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840060"
---
# <a name="inf-addpowersetting-directive"></a>INF AddPowerSetting 指令


**AddPowerSetting** 指令将引用一个或多个用于修改或创建电源设置信息的部分。 每个 *添加-电源设置部分* 定义了电源设置、电源设置的允许值、电源设置的友好名称和电源设置说明。 " *添加电源设置" 部分* 还指定每个电源方案个性的默认值。 有关电源设置和电源方案个性的详细信息，请参阅 [管理设备性能状态](../kernel/managing-device-performance-states.md)。

```inf
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

通常， *添加-电源设置部分* 包括以下指令：

-   **子组** 指令。
-   **设置** 指令
-   一个列表，其中列出了两个或多个 **值** 指令或一个 **ValueRange** 指令。
-   六个 **默认** 指令的集合。

*添加-电源设置部分* 采用以下两种可能的形式之一：

-   如果允许的电源设置值最能定义为一组两个或更多离散值，请使用 **值** 指令列表指定允许的值，如下所示：

    ```inf
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

-   如果允许的电源设置值最好定义为指定范围内的非负整数值的递增序列，请使用一个 **ValueRange** 指令指定允许的值，如下所示：

    ```inf
    [add-power-setting-section]

    [SubGroup = {subgroup-guid}] | 
    SubGroup = {subgroup-guid}, subgroup-name, subgroup-description, subgroup-icon
    Setting = {setting-guid}, [setting-name],[setting-description],[setting-icon]
    ValueRange = range-minimum-value, range-maximum-value, range-increment, [range-unit-label] 

    (Six required Default directives, each one of which has the following form)
    Default = power-scheme-personality-GUID, AC/DC-index, default-setting-index | default-setting-value 
    ...
    ```

## <a name="entries"></a>项


**注意**  除了 *值数据* 输入以外，以下所有提供字符串值的条目都可以用 [指定 AddPowerSetting 字符串输入值](#specifying-an-addpowersetting-string-entry-value)中所述的一种方式指定字符串。

 

<a href="" id="subgroup"></a>**新建子**  
子组对逻辑上相关的电源设置进行分组。

若要指定系统定义的子组，请包含 **子组** 指令并仅提供 *子组-guid* 条目。 系统定义的子组由 GUID_ *Xxx* _SUBGROUP 和 NO_SUBGROUP_GUID （在 *Wdm .h* 中定义）的常量表示。

例如，GUID_VIDEO_SUBGROUP 表示一个子组，其中包含电源方案个性的视频电源设置。 NO_SUBGROUP_GUID 常数表示不以逻辑方式归属于任何子组的设置的集合。 如果未包括 **子组** 指令，则默认情况下，此设置将添加到未以逻辑方式归属到任何子组的设置的集合。

若要定义新的子组，请包含 **子组** 指令并提供以下所需的条目： *子组-guid*、 *子组名称*、 *子组-说明* 和 *子组-图标。* 新子组的 GUID 必须是唯一的，而其他条目应尽可能描述性。

<a href="" id="subgroup-guid"></a>*子组-guid*  
必需的条目提供用于标识子组的 GUID。 此项的格式为 **{**<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>**}**，其中 "X" 是十六进制数字。

例如，系统定义的常量 GUID_VIDEO_SUBGROUP 的值为 {7516B95F-F776-4464-8C53-06167F40CC99}。 此 GUID 表示一个子组，其中包含电源方案个性的视频电源设置。

<a href="" id="subgroup-name"></a>*子组-名称*  
指定电源设置的子组名称的字符串。 如果子组是系统定义的子组，则不应提供此项。 如果子组是新的，则此项是必需的。

<a href="" id="subgroup-description"></a>*子组-说明*  
一个字符串，用于向用户描述该工作组。 如果子组是系统定义的子组，则不应提供此项。 如果子组是新的，则此项是必需的。

<a href="" id="subgroup-icon"></a>*子组-图标*  
对图标资源的引用。 如果子组是系统定义的子组，则不应提供此项。 如果子组是新的，则此项是必需的。

必须将图标资源指定为非特定语言的注册表值。 有关如何指定非特定语言的注册表值的信息，请参阅 [指定 AddPowerSetting 字符串条目值](#specifying-an-addpowersetting-string-entry-value)。

<a href="" id="setting"></a>**将**  
**设置** 指令标识部分中所有其他条目适用的设置。 "添加电源设置" 部分需要一个 **设置** 指令，在 "添加电源设置" 部分中只能有一个 **设置** 指令。 如果 INF 文件定义了多个设置，则必须在其自己的 "添加电源设置" 部分中定义每个设置。

下面是与 **设置** 指令关联的条目。

<a href="" id="setting-guid"></a>*设置-guid*  
指定表示电源设置的 GUID 的必需项。 此项的格式为 **{**<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>**}**，其中每个 "X" 都是十六进制数字。

例如，下面是一个自定义 GUID 值： {BFC0D9E9-549C-483D-AD2A-3D90C98A8B03}。

<a href="" id="setting-name"></a>*设置-名称*  
一个可选项，它指定一个字符串，该字符串包含电源设置的友好名称。 "控制面板" 中的 "**电源选项**" 向用户显示此友好名称。

<a href="" id="setting-description"></a>*设置-说明*  
一个可选项，它指定一个字符串，该字符串描述用户的电源设置以及该设置对系统电源和性能的影响。

<a href="" id="setting-icon"></a>*设置-图标*  
作为对图标资源的引用的可选项。 图标资源必须由非特定语言的注册表值指定。

有关如何指定非特定语言的注册表值的信息，请参阅 [指定 AddPowerSetting 字符串条目值](#specifying-an-addpowersetting-string-entry-value)。

<a href="" id="value"></a>**负值**  
**值** 指令为电源设置定义允许的值。 如果可以将值最好定义为两个或更多值的集合（其中每个值都可以具有特定于值的自定义数据类型），则应使用 **value** 指令。 在这种情况下，添加-电源设置部分应包含两个或多个 **值** 指令。 用户可以在 "控制面板" 的 " **电源选项** " 中选择其中一个值，以配置电源方案。

如果可以将允许的电源设置值最好地描述为范围内的一组递增的非负整数，请使用 **ValueRange** 指令而不是 **值** 指令来指定允许的电源设置值。

<a href="" id="value-index"></a>*值索引*  
指定唯一索引值的必需项，该索引值大于或等于零，用于引用相应的设置值。 控制面板中的 "**电源选项**" 按其对应索引值从低到高的顺序向用户显示电源设置值。

<a href="" id="value-name"></a>*值-名称*  
一个必需项，它提供为相应的设置值提供友好名称的字符串。 控制面板中的 "**电源选项**" 将电源设置值的友好名称显示给用户。

<a href="" id="value-description"></a>*值-说明*  
一个可选项，它提供一个字符串，该字符串向用户描述电源设置值以及设置值对系统电源和性能的影响。

<a href="" id="value-flags"></a>*值标志*  
一个必需的项，它指定相应的值数据输入的数据类型，如下表所示。

| 标志值 | 数据类型   |
|------------|-------------|
| 0x00000001 | [REG_BINARY](/windows/desktop/SysInfo/registry-value-types) |
| 0x00010001 | REG_DWORD   |
| 0x00000000 | [REG_SZ](/windows/desktop/SysInfo/registry-value-types)     |

 

<a href="" id="value-data"></a>*值-数据*  
为相应的设置值提供数据的必需项，其格式取决于相应的 *值标志* 条目指定的数据类型，如下所示：

-   可以使用0x 表示法以十六进制格式指定 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types) 值，也可以使用不带0x 表示法的成对十六进制数字的以逗号分隔的列表来指定。

    例如，以下项是等效的：0xFEDCBA9876543210 和以逗号分隔的成对十六进制数字列表： FE、DC、BA、98、76、54、32、10。

-   可以使用0x 表示法) 或十进制格式，以十六进制格式指定 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types) 值 (。
-   [REG_SZ](/windows/desktop/SysInfo/registry-value-types)值只能表示为括在双引号中的字符串 ( "*带引号的字符串*" ) ，或者表示为 INF 文件的 "inf [**字符串**](inf-strings-section.md)" 部分中定义的%*strkey*% 令牌。

**注意**  不应使用字符串值，因为不能对其进行本地化。 请改用 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types) 或 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)类型的值。

 

<a href="" id="valuerange"></a>**ValueRange**  
如果允许的电源设置值最好定义为指定范围内的非负整数值的递增序列，请使用 **ValueRange** 指令。 Power manager 验证用户在 "控制面板" 的 " **电源选项** " 中选择的设置是否为以下允许值之一。 允许的值集由最小允许值、最大允许值和范围内允许的值之间的增量决定。 如果值满足以下值，则允许该值：

```inf
range-minimum-value + k*range-increment
```

其中， *范围最小值* 大于或等于零， *k* 和 *范围增量* 大于或等于1，并且值小于或等于 *范围-最大值*。 此外，*范围最大值* 应等于值 k 范围的最 *小值*  +  *k* \* *范围*。

例如，对于 *最小值* 等于0，范围 *上限值* 等于10， *范围增量* 等于2，允许的值如下所示：0、2、4、6、8和10。

如果可以将允许的电源设置值最好地描述为值列表，其中每个值都可以具有特定于值的自定义数据类型，请使用 **value** 指令而不是 **ValueRange** 指令。

<a href="" id="range-minimum-value"></a>*范围-最小值*  
[REG_DWORD](/windows/desktop/SysInfo/registry-value-types)类型的值，该值指定允许的最小电源设置。

<a href="" id="range-maximum-value"></a>*范围-最大值*  
[REG_DWORD](/windows/desktop/SysInfo/registry-value-types)类型的值，该值指定最大允许的电源设置值。 最大值必须大于或等于最小值，并且应等于大于零的部分整数 *k* 的范围-最小值 + *k \* 范围增量*。

<a href="" id="range-increment-"></a>*范围-递增*   
一个大于零的类型 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types) 的值。 此值指定由 *范围最小值* 和 *范围最大值* 指定的非独占范围内连续值之间的差异。

<a href="" id="range-unit-label-"></a>*范围-单位标签*   
描述电源设置值的可选字符串。 字符串与 *设置名称* 一起通知用户要输入的数据类型。

例如，该字符串可用于指定值单位，例如 "分钟" 或 "%" (表示百分比) 。

<a href="" id="default"></a>**缺省值**  
**AddPowerSetting** 部分必须包含六个 **默认** 指令。 **默认** 指令为应用到 AC 电源状态的三个系统定义的电源方案个性中的一个，以及适用于 DC 电源状态的三个系统定义的电源方案个性指定默认值。

默认值为有效且准确，这一点非常重要。 如果用户未手动设置电源设置，则 power manager 将使用 **默认** 指令指定的默认值。

<a href="" id="power-scheme-personality-guid"></a>*电源方案-个性-GUID*  
以下 Guid 之一，用于标识默认值应用于的电源方案。

| 个性      | GUID                                   |
|------------------|----------------------------------------|
| “节能程序”      | {A1841308-3541-4FAB-BC81-F71556F20B4A} |
| 高性能 | {8C5E7FDA-E8BF-4A96-9A85-A6E23A8C635C} |
| 已平衡         | {381B4222-F694-41F0-9685-FF5BB260DF2E} |

 

这些 Guid 在 *Wdm* 中定义。

<a href="" id="ac-dc-index"></a>*AC/DC-索引*  
如果 *ac/dc 索引* 为0，则该设置将应用到 ac 电源状态，如果 *ac/dc-索引* 为1，则该设置将应用于 DC 电源状态。 0或1以外的值无效。

<a href="" id="default-setting-index-"></a>*默认设置-索引*   
如果 **值** 指令用于指定允许值，则 *默认设置-索引* 为 **值** 指令的 *值索引项* 的值。 如果 **ValueRange** 指令用于指定允许的值，则此项不适用。

<a href="" id="default-setting-value-"></a>*默认设置-值*   
如果 **ValueRange** 指令用于指定允许值，则 *默认值设置* 为 **ValueRange** 指令指定的允许值之一。 如果 **值** 指令用于指定允许的值，则此项不适用。

<a name="remarks"></a>备注
-------

在 INF 文件中， *添加-电源设置节* 名称必须是唯一的，但它可以在同一 INF 文件中由多个 **AddPowerSetting** 指令引用。 每个节名称必须遵循 [INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中描述的常规规则。

卸载设备后，电源管理器不会自动删除设备电源策略。 可以通过在 *Powrprof* 中定义的系统提供的电源设置例程来安装或删除电源设置、值和默认值。 有关这些电源管理例程的详细信息，请参阅随 Microsoft Windows SDK 文档提供的电源管理参考。

此外， *Powercfg.exe* 命令行工具可用于更改电源设置。 有关 *Powercfg.exe* 的信息，请参阅 Microsoft 帮助和支持中心。

有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

### <a name="specifying-an-addpowersetting-string-entry-value"></a>指定 AddPowerSetting 字符串条目值

除了类型 [REG_SZ](/windows/desktop/SysInfo/registry-value-types)的 *值数据* 输入以外，使用 **AddPowerSetting** 指令提供的所有其他字符串输入值都可以表示为用双引号引起来的字符串 ( "*带引号的字符串*" ) ，作为在 inf 文件的 inf 字符串部分中定义的%*strkey*% 令牌，或作为非特定语言的注册表值。

非特定语言的注册表值用于支持 (MUI) 的 Windows 多语言用户界面，并按如下所示指定：

```inf
"@file-path,-resourceID[;comment]"
```

指定非特定语言的注册表值的条目如下所示：

<a href="" id="file-path"></a>*文件路径*  
包含资源的文件的完全限定路径。

<a href="" id="resourceid"></a>*resourceID*  
相应资源的资源 ID。 对于字符串， *resourceID* 引用字符串。 对于图标， *resourceID* 引用一个图标。

<a href="" id="comment"></a>*条*  
可用于帮助调试或提供有关设置的其他注释的可选值。 对于字符串资源，电源管理器不会结合或显示带有指定资源字符串的注释字符串。

有关如何指定非特定语言的注册表值的详细信息，请参阅 [呈现 Shell 和注册表字符串](/previous-versions//ms776232(v=vs.85))。

<a name="examples"></a>示例
--------

以下两个示例定义了控制 LCD 亮度的电源设置。 第一个示例演示如何使用 **Value** 指令定义最小值、中等值和最大 LCD 亮度值。

```inf
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

第二个示例演示如何使用 **ValueRange** 指令来定义一系列允许的 LCD 亮度值，这些值在0% 到100% 之间有所不同，在允许值之间增加1%。

```inf
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

## <a name="see-also"></a>请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**_DDInstall_。HW**](inf-ddinstall-hw-section.md)

[**_DDInstall_。接口**](inf-ddinstall-interfaces-section.md)

[**_DDInstall_。服务器**](inf-ddinstall-services-section.md)

