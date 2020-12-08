---
title: DevCon Status
description: 显示计算机上设备的驱动程序的 "正在运行"、"已停止" 或 ") 已禁用" 状态 (状态。 在本地和远程计算机上有效。
keywords:
- DevCon 状态驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Status
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30c6bb8fdd496208a17df66992c5401d400e06ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783343"
---
# <a name="devcon-status"></a>DevCon Status

显示计算机上设备的驱动程序的 "正在运行"、"已停止" 或 ") 已禁用" 状态 (状态。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] status {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_status_toolsspanspan-idddk_devcon_status_toolsspanparameters"></a><span id="ddk_devcon_status_tools"></span><span id="DDK_DEVCON_STATUS_TOOLS"></span>参数

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

<span id="________class______"></span><span id="________CLASS______"></span>**=**_类_ 指定设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于操作名称之前 (**状态**) 。 否则，DevCon 将忽略 **/m** 参数，并在本地计算机上显示设备驱动程序的状态，而不会返回语法错误。

如果 DevCon 无法确定设备的状态，例如，当设备不再连接到计算机时，DevCon 将从状态显示中省略描述状态的行。

下面的示例显示成功的状态命令。 描述设备状态的文本以粗体显示。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
    Driver is running.
1 matching device(s) found.
```

与此相反，下面的示例演示了 DevCon 如何显示设备找不到的状态。 显示中缺少状态说明。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
1 matching device(s) found.
```

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon /m:\\Server01 status *
devcon status pci*
devcon status "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon status =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例17：显示本地计算机上所有设备的状态](devcon-examples.md#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[示例18：按设备实例 ID 显示设备状态](devcon-examples.md#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[示例19：显示远程计算机上相关设备的状态](devcon-examples.md#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)
