---
title: DevCon Remove
description: 从设备树中删除设备并删除设备的设备堆栈。
ms.assetid: 02236d0d-4628-4b5b-9a15-331905f07358
keywords:
- DevCon 删除驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Remove
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfce95f5140893c2ff0e1d4fa7fc3f03e2b399c2
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492508"
---
# <a name="devcon-remove"></a>DevCon Remove


从设备树中删除设备并删除设备的设备堆栈。 由于这些操作，从设备树中删除子设备和支持的设备的驱动程序都会被卸载。

此操作不会删除设备驱动程序或为该设备安装的任何文件。 从设备树中删除设备之后, 的文件保持和设备仍在内部表示为可重新枚举虚幻设备。

仅在本地计算机上有效。

```
    devcon [/r] remove {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconremovetoolsspanspan-idddkdevconremovetoolsspanparameters"></a><span id="ddk_devcon_remove_tools"></span><span id="DDK_DEVCON_REMOVE_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

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
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>'*PNP0600</strong>，其中 *PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>  



<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>类</em>指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，添加条件的重新启动参数 (/ r) 命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon /r remove "PCI\VEN_8086&DEV_7110" 
devcon /r remove =printer
devcon /r remove =printer *deskj*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 35:通过设备实例 ID 模式中删除的设备](devcon-examples.md#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[示例 36:删除特定网络设备](devcon-examples.md#ddk_example_36_remove_a_particular_network_device_tools)









