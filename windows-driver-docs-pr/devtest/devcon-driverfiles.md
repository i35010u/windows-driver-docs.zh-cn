---
title: DevCon DriverFiles
description: 显示已安装的 INF 文件和指定的设备的设备驱动程序文件的完整路径和文件名称。 仅在本地计算机上有效。
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
ms.openlocfilehash: f64e8f641ad6db19cc84d5f47d1149e7f85815b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533621"
---
# <a name="devcon-driverfiles"></a>DevCon DriverFiles


显示已安装的 INF 文件和指定的设备的设备驱动程序文件的完整路径和文件名称。 仅在本地计算机上有效。

```
    devcon driverfiles {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevcondriverfilestoolsspanspan-idddkdevcondriverfilestoolsspanparameters"></a><span id="ddk_devcon_driverfiles_tools"></span><span id="DDK_DEVCON_DRIVERFILES_TOOLS"></span>参数


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
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (<strong></em></strong>) 创建 ID 模式，例如， <strong><em>磁盘</em></strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>例如，指示设备实例 ID <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>&#39;</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>&#39;* PNP0600</strong>，其中 * PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>类</em>指定设备的设备安装程序类。 等号 (**=**) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**DevCon DriverFiles**操作仅在本地计算机上运行。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon driverfiles *
devcon driverfiles FDC\GENERIC_FLOPPY_DRIVE pci*
devcon driverfiles =media
devcon driverfiles =media isapnp*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 8:列出所有驱动程序文件](devcon-examples.md#ddk_example_8_list_all_driver_files_tools)

[示例 9:列出特定设备的驱动程序文件](devcon-examples.md#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)









