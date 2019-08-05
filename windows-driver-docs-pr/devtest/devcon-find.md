---
title: DevCon Find
description: 查找当前连接到计算机的所有设备。 显示设备实例 ID 和设备说明。 在本地和远程计算机上有效。
ms.assetid: ecd72b34-4117-4360-95d2-e87702f025a1
keywords:
- DevCon 查找驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Find
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57439bce9647b5d4a26f256c80e2ab994f7ee54e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347667"
---
# <a name="devcon-find"></a>DevCon Find


查找当前连接到计算机的所有设备。 显示设备实例 ID 和设备说明。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] find {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddk_devcon_find_toolsspanspan-idddk_devcon_find_toolsspanparameters"></a><span id="ddk_devcon_find_tools"></span><span id="DDK_DEVCON_FIND_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="______________"></span> **\\** *   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id ( **&** ) 必须括在引号中。

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



<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>类</em>指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**查找**)。 否则，将忽略 DevCon **/m**参数并在其中搜索本地计算机而不返回语法错误。

可以使用**DevCon 查找**操作来查找当前未通过指定完整的设备实例 ID 的设备连接到计算机的设备而硬件 ID 或 ID 的模式。 指定完整的设备实例 ID 重写上的限制**DevCon 查找**操作，用于限制到连接的设备。

**DevCon 查找**使用单个类自变量的操作都是作为相同[ **DevCon ListClass** ](devcon-listclass.md)操作。

若要查找的所有设备，包括当前未连接到计算机，请使用[ **DevCon FindAll** ](devcon-findall.md)操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon find *
devcon find =media *pnp*
devcon /m:\\Server01 find *mou* 
devcon find @*hub*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 20:查找设备硬件 ID 模式](devcon-examples.md#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[示例 21:查找设备通过设备实例 ID 或类](devcon-examples.md#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)









