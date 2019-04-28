---
title: DevCon Enable
description: 允许设备在计算机上。 仅在本地计算机上有效。若要启用设备意味着设备驱动程序加载到内存，设备便可供使用。
ms.assetid: 2fb2cb9b-ba37-4946-b78b-0cd2aaaadcb4
keywords:
- DevCon 启用驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Enable
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf1da4bd48435d50a2829d39109cb9cddd5a118a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347674"
---
# <a name="devcon-enable"></a>DevCon Enable


允许设备在计算机上。 仅在本地计算机上有效。

向*启用*设备意味着设备驱动程序加载到内存和设备便可供使用。

```
    devcon [/r] enable {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconenabletoolsspanspan-idddkdevconenabletoolsspanparameters"></a><span id="ddk_devcon_enable_tools"></span><span id="DDK_DEVCON_ENABLE_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

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



<span id="________class______"></span><span id="________CLASS______"></span> *=class*   
指定设备的设备安装程序类。 等号 (**=**) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

DevCon 启用设备，即使已启用。 之前和之后启用设备，使用[ **DevCon 状态**](devcon-status.md)操作来验证设备状态。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，添加条件的重新启动参数 (/ r) 命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon enable * (not recommended)
devcon /r enable *DVD-ROM* 
devcon /r enable =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 28:启用特定设备](devcon-examples.md#ddk_example_28_enable_a_particular_device_tools)

[示例 29:使设备由类](devcon-examples.md#ddk_example_29_enable_devices_by_class_tools)









