---
title: DevCon Disable
description: 禁用计算机上的设备。
keywords:
- DevCon 禁用驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Disable
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30525fcc4140d8ade538b2a93ee8722a59c421c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817803"
---
# <a name="devcon-disable"></a>DevCon Disable

禁用计算机上的设备。 仅在本地计算机上有效。

若要 *禁用* 设备，意味着设备仍保持物理连接到计算机，但其驱动程序已从内存中卸载，其资源被释放，因此无法使用该设备。

```
    devcon [/r] disable {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_disable_toolsspanspan-idddk_devcon_disable_toolsspanparameters"></a><span id="ddk_devcon_disable_tools"></span><span id="DDK_DEVCON_DISABLE_TOOLS"></span>参数

<span id="________r______"></span><span id="________R______"></span>**/r** 条件重启。 仅当需要重新启动才能使更改生效时，才能在完成操作后重新启动系统。

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

<span id="________class______"></span><span id="________CLASS______"></span>**=**<em>类</em>指定设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

DevCon 禁用设备，即使设备已禁用。 禁用设备之前和之后，请使用 [**DevCon 状态**](devcon-status.md) 操作来验证设备状态。

使用 ID 模式禁用设备之前，请确定哪些设备将受到影响。 若要执行此操作，请在显示命令中使用模式，如 **devcon STATUS \\ usb** _ 或 _*devcon hwid \\ USB* *_。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，请将 (/r) 的条件重新启动参数添加到命令中。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon disable _ (not recommended)
devcon /r disable *DVD-ROM*
devcon /r disable =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例30：按 ID 模式禁用设备](devcon-examples.md#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[示例31：按设备实例 ID 禁用设备](devcon-examples.md#ddk_example_31_disable_devices_by_device_instance_id_tools)
