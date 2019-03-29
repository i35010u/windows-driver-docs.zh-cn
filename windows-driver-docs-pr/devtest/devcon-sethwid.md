---
title: DevCon SetHwID
description: 添加、 删除和更改的硬件 Id 的本地或远程计算机上的根枚举设备的顺序。
ms.assetid: 79948ff0-8b30-4a64-beea-e3f08aef7170
keywords:
- DevCon SetHwID 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon SetHwID
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25fb7501bde304f36b5fcf3868455ee8f2c022cd
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349117"
---
# <a name="devcon-sethwid"></a>DevCon SetHwID


添加、 删除和更改的硬件 Id 的本地或远程计算机上的根枚举设备的顺序。

```
    devcon [/m:\\computer] sethwid {* | ID [ID ...] | =class [ID [ID ...]]} := [ = | + | - | ! ]HardwareIDs ...
```

## <a name="span-idddkdevconsethwidtoolsspanspan-idddkdevconsethwidtoolsspanparameters"></a><span id="ddk_devcon_sethwid_tools"></span><span id="DDK_DEVCON_SETHWID_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\**<em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="______________"></span> **\\***   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id (**&**) 必须括在引号中。

以下特殊字符修改 ID 参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (</em>) 创建 ID 模式，例如，<em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>例如，指示设备实例 ID <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上<strong>' * PNP0600</strong>，其中 * PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>类</em>指定根枚举设备的设备安装程序类。 等号 (**=**) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

<span id="_______HardwareIDs______"></span><span id="_______hardwareids______"></span><span id="_______HARDWAREIDS______"></span> *HardwareIDs*   
指定一个或多个硬件 Id。

如果硬件 Id 前面没有符号参数 (**+**， **-**， **=**， **！**)DevCon 添加或移动到指定的顺序中的设备硬件 Id 的列表的末尾指定的硬件 Id。 这相当于-参数。

<span id="_"></span>=  
替换指定的顺序指定的硬件 Id 的设备的硬件 Id 列表。

<span id="______________"></span> **+**   
添加或移动到的设备的硬件 Id 列表的开头指定的硬件 Id。

<span id="_______-______"></span> **-**   
添加或移动到的设备硬件 Id 列表的末尾指定的硬件 Id。

<span id="______________"></span> **!**   
从设备的硬件 Id 的列表中删除指定的硬件 Id。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

一个*根枚举*设备是设备出现在根注册表子项 (HKEY\_本地\_机\\系统\\*ControlSet* \\枚举\\根)。

您可以在每个命令中指定多个硬件 Id。 **！** （删除） 参数仅适用于它加上前缀的硬件 ID。 其他符号参数适用于所有的硬件 Id，请按照之前在命令中的下一步符号参数。

DevCon 移动，而不是增加了，如果已指定的硬件 ID 的硬件 ID 中存在的设备的硬件 Id 列表。

为成功消息**DevCon SetHwIDs**命令报告的设备 （或设备列表），它在其中后修改的硬件 Id，不是修改后的硬件 Id 的数目数。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon sethwid @ROOT\LEGACY* := legacy
devcon sethwid @ROOT\LEGACY_AFD\0000 := =afd1 afd2 afd3
devcon sethwid legacy := devtype3 -devtype4
devcon sethwid legacy afd1 := +devtype3
devcon sethwid @ROOT\LEGACY_BEEP\0000 := !beep legacy
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 40:将硬件 ID 分配给旧的设备](devcon-examples.md#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[示例 41:添加到远程计算机上的所有旧设备的硬件 ID](devcon-examples.md#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[示例 42:从远程计算机上的所有旧设备中删除硬件 ID](devcon-examples.md#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[示例 43:添加、 删除和替换的硬件 Id](devcon-examples.md#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[示例 44:强制更新 HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)









