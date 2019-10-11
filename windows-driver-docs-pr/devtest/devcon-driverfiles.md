---
title: DevCon DriverFiles
description: 显示指定设备的已安装 INF 文件和设备驱动程序文件的完整路径和文件名。 仅在本地计算机上有效。
ms.assetid: 8f8394e4-1ee4-4356-9f4d-ecc70deeaab1
keywords:
- DevCon DriverFiles 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon DriverFiles
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f5e23f828e1e0b38dc37b4bc6b4a26ffa2c79f
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038093"
---
# <a name="devcon-driverfiles"></a>DevCon DriverFiles

显示指定设备的已安装 INF 文件和设备驱动程序文件的完整路径和文件名。 仅在本地计算机上有效。

```
    devcon driverfiles {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_driverfiles_toolsspanspan-idddk_devcon_driverfiles_toolsspanparameters"></a><span id="ddk_devcon_driverfiles_tools"></span><span id="DDK_DEVCON_DRIVERFILES_TOOLS"></span>Parameters

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
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符（<strong> @ no__t）创建 ID 模式，例如<strong><em>disk</em></strong>。</p></td>
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

**DevCon DriverFiles**操作仅在本地计算机上运行。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon driverfiles *
devcon driverfiles FDC\GENERIC_FLOPPY_DRIVE pci*
devcon driverfiles =media
devcon driverfiles =media isapnp*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[Example 8：列出所有驱动程序文件 @ no__t-0

[Example 9：列出特定设备的驱动程序文件 @ no__t
