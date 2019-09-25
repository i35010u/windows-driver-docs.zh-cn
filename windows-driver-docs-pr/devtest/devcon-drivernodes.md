---
title: DevCon DriverNodes
description: 列出与设备兼容的所有驱动程序包及其版本和排名。 仅在本地计算机上有效。
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
ms.openlocfilehash: 7899295f10dd5bffd7241a8af130c2ccf83c5db9
ms.sourcegitcommit: 2aa583e3da4ae9338a0d11678bf77f1460286f2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "69976074"
---
# <a name="devcon-drivernodes"></a>DevCon DriverNodes


列出与设备兼容的所有[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)及其版本和排名。 仅在本地计算机上有效。

```
    devcon drivernodes {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddk_devcon_drivernodes_toolsspanspan-idddk_devcon_drivernodes_toolsspanparameters"></a><span id="ddk_devcon_drivernodes_tools"></span><span id="DDK_DEVCON_DRIVERNODES_TOOLS"></span>Parameters


<span id="______________"></span> **\\** *   
表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span>*ID*   
指定设备的所有或部分硬件 ID、兼容 ID 或设备实例 ID。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含 "&" 符（ **&** ）的 id 必须用引号引起来。

以下特殊字符修改 ID 参数。

<table>  
<colgroup><col width="50%" /> <col width="50%" /></colgroup>  
<thead>  
<tr class="header">  
<th align="left">字符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符（<strong></em></strong>）创建 ID 模式，例如<strong><em>磁盘</em></strong>。</p></td>
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



<span id="________class______"></span><span id="________CLASS______"></span> **=** _类_   
指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**DevCon DriverNodes**操作仅在本地计算机上运行。

**DevCon DriverNodes**操作特别适用于疑难解答安装问题。 例如，你可以使用它来确定是否为设备使用了 Windows INF 文件或自定义的第三方 INF 文件。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon drivernodes *
devcon drivernodes *miniport*
devcon drivernodes =usb pci* usb*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例10：按硬件 ID 模式列出驱动程序包](devcon-examples.md#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[示例11：按设备实例 ID 模式列出驱动程序包](devcon-examples.md#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)









