---
title: DevCon HwIDs
description: 显示的硬件 Id、 兼容 Id 和设备实例 Id 的指定设备。 在本地和远程计算机上有效。
ms.assetid: b76de01e-fedf-41c2-ba2e-837b442ab93f
keywords:
- DevCon HwIDs 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon HwIDs
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011bd34e2fe64b228485b341bed5330079ff1620
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348317"
---
# <a name="devcon-hwids"></a>DevCon HwIDs


显示的硬件 Id、 兼容 Id 和设备实例 Id 的指定设备。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] hwids {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconhwidstoolsspanspan-idddkdevconhwidstoolsspanparameters"></a><span id="ddk_devcon_hwids_tools"></span><span id="DDK_DEVCON_HWIDS_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\**<em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="______________"></span> **\\***   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
通过使用标识符来指定一个或多个设备。

键入全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id (**&**) 必须括在引号中。

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
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (<strong></em></strong>) 创建 ID 模式，例如， <strong><em>磁盘</em></strong>。</p></td>
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



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>类</em>指定通过使用安装程序类的一个或多个设备。

键入全部或部分设备的安装程序类的名称。 等号 (**=**) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**hwids**)。 否则，将忽略 DevCon **/m**参数，并显示不带返回语法错误的本地计算机上的设备的硬件 Id。

若要创建根枚举设备的硬件 ID，请使用[ **DevCon SetHwID** ](devcon-sethwid.md)命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon hwids *
devcon /m:\\server01 hwids acpi* 
devcon hwids acpi* *port*
devcon hwids =usb
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 1:查找所有硬件 Id](devcon-examples.md#ddk_example_1_find_all_hardware_ids_tools)

[示例 2:通过使用一种模式中找到硬件 Id](devcon-examples.md#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[示例 3:通过使用类找到硬件 Id](devcon-examples.md#ddk_example_3_find_hardware_ids_by_using_a_class_tools)









