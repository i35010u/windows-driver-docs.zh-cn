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
ms.openlocfilehash: 09e57ccfd171567ba78e37baa69225c97fbb3e65
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038084"
---
# <a name="devcon-find"></a>DevCon Find

查找当前连接到计算机的所有设备。 显示设备实例 ID 和设备说明。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] find {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_find_toolsspanspan-idddk_devcon_find_toolsspanparameters"></a><span id="ddk_devcon_find_tools"></span><span id="DDK_DEVCON_FIND_TOOLS"></span>Parameters

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m： \\ @ no__t**<em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。

<span id="______________"></span> **\*** 表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span>*ID*指定设备的硬件 id、兼容 ID 或设备实例 id 的全部或部分。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含 "&" 符（ **&** ）的 id 必须用引号引起来。

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
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符（</em>）创建 ID 模式，例如<em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>指示设备实例 ID，例如<strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义（与它显示的完全相同）匹配字符串。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>'*PNP0600</strong>，其中 *PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>

<span id="________class______"> @ no__t-1<span id="________CLASS______"> </span> **@no__t**<em>指定设备</em>的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M**参数必须位于操作名称（**find**）之前。 否则，DevCon 将忽略 **/m**参数，并在本地计算机上搜索，而不返回语法错误。

你可以使用**DevCon find**操作来查找当前未连接到计算机的设备，方法是指定设备的完整设备实例 ID，而不是指定硬件 ID 或 ID 模式。 指定完整的设备实例 ID 将覆盖**DevCon Find**操作的限制，以将其限制到附加设备。

使用单个 class 参数的**DevCon Find**操作与[**DevCon ListClass**](devcon-listclass.md)操作相同。

若要查找所有设备，包括当前未连接到计算机的设备，请使用[**DevCon FindAll**](devcon-findall.md)操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon find *
devcon find =media *pnp*
devcon /m:\\Server01 find *mou*
devcon find @*hub*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[Example 20：按硬件 ID 模式查找设备 @ no__t-0

[Example 21：按设备实例 ID 或类 @ no__t 查找设备-0
