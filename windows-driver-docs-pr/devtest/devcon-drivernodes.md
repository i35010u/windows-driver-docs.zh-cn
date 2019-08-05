---
title: DevCon DriverNodes
description: 列出了所有与该设备，以及它们的版本和排名兼容的驱动程序包。 仅在本地计算机上有效。
ms.assetid: 891aa022-44f5-4920-ab57-a0573deb94de
keywords:
- DevCon DriverNodes 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon DriverNodes
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c70290635a84b60b11a51d3c3a054b234c8cf38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371401"
---
# <a name="devcon-drivernodes"></a>DevCon DriverNodes


列出所有[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)兼容的设备，以及它们的版本和排名。 仅在本地计算机上有效。

```
    devcon drivernodes {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddk_devcon_drivernodes_toolsspanspan-idddk_devcon_drivernodes_toolsspanparameters"></a><span id="ddk_devcon_drivernodes_tools"></span><span id="DDK_DEVCON_DRIVERNODES_TOOLS"></span>参数


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
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (<strong></em></strong>) 创建 ID 模式，例如， <strong><em>磁盘</em></strong>。</p></td>
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

**DevCon DriverNodes**操作仅在本地计算机上运行。

**DevCon DriverNodes**操作是特别是一些有助于解决安装问题。 例如，您可以使用它来确定是否 Windows INF 文件或自定义的第三方 INF 文件使用的设备。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon drivernodes *
devcon drivernodes *miniport*
devcon drivernodes =usb pci* usb*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 10:列表由硬件 ID 模式的驱动程序包](devcon-examples.md#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[示例 11:通过设备实例 ID 模式列表驱动程序包](devcon-examples.md#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)









