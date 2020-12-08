---
title: DevCon SetHwID
description: 添加、删除和更改本地或远程计算机上根枚举设备的硬件 Id 的顺序。
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
ms.openlocfilehash: 11304f5938ed4d719e4dfd919af427f45c8b1595
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783353"
---
# <a name="devcon-sethwid"></a>DevCon SetHwID

添加、删除和更改本地或远程计算机上根枚举设备的硬件 Id 的顺序。

```
    devcon [/m:\\computer] sethwid {* | ID [ID ...] | =class [ID [ID ...]]} := [ = | + | - | ! ]HardwareIDs ...
```

## <a name="span-idddk_devcon_sethwid_toolsspanspan-idddk_devcon_sethwid_toolsspanparameters"></a><span id="ddk_devcon_sethwid_tools"></span><span id="DDK_DEVCON_SETHWID_TOOLS"></span>参数

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span>**/m： \\ \\**<em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**   若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。

<span id="______________"></span> **\** _ 表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> _ID * 指定设备的硬件 ID、兼容 ID 或设备实例 ID 的全部或部分。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含与号字符 () 的 Id **&** 必须用引号引起来。

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
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符 (</em>) 创建 ID 模式，例如 <em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>指示设备实例 ID，例如 <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p> (单引号) </p></td>
<td align="left"><p>按原义 (与) 显示的内容完全匹配。 在字符串前面加上单引号，指示星号是 ID 名称的一部分，并且不是通配符，例如 <strong>"* PNP0600</strong>，其中，* PNP0600 (包括星号) 为硬件 ID。</p></td>
</tr>
</tbody>
</table>

<span id="________class______"></span><span id="________CLASS______"></span>**=**<em>类</em>指定根枚举设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

<span id="_______HardwareIDs______"></span><span id="_______hardwareids______"></span><span id="_______HARDWAREIDS______"></span>*HardwareIDs* 指定一个或多个硬件 Id。

如果硬件 id 前面没有符号参数 (**+** 、 **-** 、 **=** 、 **！**) ，则 DevCon 会按指定顺序将指定的硬件 id 添加到设备的硬件 id 列表的末尾。 这等效于-参数。

<span id="_"></span>=  
按指定顺序将设备的硬件 Id 列表替换为指定的硬件 Id。

<span id="______________"></span>**+** 将指定的硬件 id 添加或移动到设备硬件 id 列表的开头。

<span id="_______-______"></span>**-** 将指定的硬件 id 添加或移动到设备的硬件 id 列表的末尾。

<span id="______________"></span> **!**
从设备的硬件 Id 列表中删除指定的硬件 Id。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

*根枚举* 设备是出现在根注册表子项中的设备， (HKEY \_ LOCAL \_ MACHINE \\ System \\ *ControlSet* \\ Enum \\ root) 。

可以在每个命令中指定多个硬件 Id。 重载 **!**  (delete) 参数仅适用于其前缀的硬件 ID。 其他符号参数适用于在命令中的下一个符号参数之前跟随的所有硬件 Id。

如果指定的硬件 ID 已存在于设备的硬件 id 列表中，则 DevCon 会移动而不是添加硬件 ID。

**DevCon SetHwIDs** 命令的成功消息将报告已修改硬件 id)  (设备的数量，而不是已修改硬件 id 的数量。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon sethwid @ROOT\LEGACY* := legacy
devcon sethwid @ROOT\LEGACY_AFD\0000 := =afd1 afd2 afd3
devcon sethwid legacy := devtype3 -devtype4
devcon sethwid legacy afd1 := +devtype3
devcon sethwid @ROOT\LEGACY_BEEP\0000 := !beep legacy
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例40：向旧设备分配硬件 ID](devcon-examples.md#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[示例41：向远程计算机上的所有旧设备添加硬件 ID](devcon-examples.md#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[示例42：从远程计算机上的所有旧设备中删除硬件 ID](devcon-examples.md#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[示例43：添加、删除和替换硬件 Id](devcon-examples.md#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[示例44：强制更新 HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)
