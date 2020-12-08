---
title: DevCon Stack
description: 显示指定设备的预期驱动程序堆栈，以及每个设备的设备安装程序类的 GUID 和名称。
keywords:
- DevCon Stack 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Stack
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2187dc63c6c6def5e66557a5aaf66e1ed08a56a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783347"
---
# <a name="devcon-stack"></a>DevCon Stack

显示指定设备的预期驱动程序堆栈，以及每个设备的设备安装程序类的 GUID 和名称。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] stack {* | ID [ID ...] | =class [ID [ID...]]}
```

## <a name="span-idddk_devcon_stack_toolsspanspan-idddk_devcon_stack_toolsspanparameters"></a><span id="ddk_devcon_stack_tools"></span><span id="DDK_DEVCON_STACK_TOOLS"></span>参数

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

<span id="________class______"></span><span id="________CLASS______"></span>**=**<em>类</em>指定设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。 你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于操作名称 (**stack**) 之前。 否则，DevCon 将忽略 **/m** 参数，并在本地计算机上显示设备驱动程序的堆栈，而不会返回语法错误。

**DevCon Stack** 操作显示设备的预期驱动程序堆栈。 尽管实际的驱动程序堆栈通常与预期的堆栈匹配，但有可能变体。

要调查设备问题，请将堆栈操作所需的驱动程序堆栈与设备使用的实际驱动程序进行比较，如 [**DevCon DriverFiles**](devcon-driverfiles.md) 操作所示。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon /m:\\Server01 stack * > Server01Stack.txt
devcon stack ISAPNP\ReadDataPort
devcon /m:\\Server01 stack pci*
devcon stack =multifunction
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例14：显示存储设备的驱动程序堆栈](devcon-examples.md#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[示例15：查找设备的安装程序类](devcon-examples.md#ddk_example_15_find_the_setup_class_of_a_device_tools)

[示例16：在远程计算机上显示相关设备的堆栈](devcon-examples.md#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)
