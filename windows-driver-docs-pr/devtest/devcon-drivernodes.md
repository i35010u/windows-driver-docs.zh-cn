---
title: DevCon DriverNodes
description: 列出与设备兼容的所有驱动程序包及其版本和排名。 仅在本地计算机上有效。
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
ms.openlocfilehash: 39d32b0bbe2302cb610a656181ed91b022e6b43c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798327"
---
# <a name="devcon-drivernodes"></a>DevCon DriverNodes

列出与设备兼容的所有 [驱动程序包](../install/components-of-a-driver-package.md) 及其版本和排名。 仅在本地计算机上有效。

```
    devcon drivernodes {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_drivernodes_toolsspanspan-idddk_devcon_drivernodes_toolsspanparameters"></a><span id="ddk_devcon_drivernodes_tools"></span><span id="DDK_DEVCON_DRIVERNODES_TOOLS"></span>参数

<span id="______________"></span> **\** _ 表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> _ID * 指定设备的硬件 ID、兼容 ID 或设备实例 ID 的全部或部分。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含与号字符 () 的 Id **&** 必须用引号引起来。

以下特殊字符修改 ID 参数。

<table>  
<colgroup> <col width="50%" /> <col width="50%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">字符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符 (<strong> </em></strong>) 创建 ID 模式，例如<strong><em>磁盘</em></strong>。</p></td>
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

<span id="________class______"></span><span id="________CLASS______"></span>**=**_类_ 指定设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**DevCon DriverNodes** 操作仅在本地计算机上运行。

**DevCon DriverNodes** 操作特别适用于疑难解答安装问题。 例如，你可以使用它来确定是否为设备使用了 Windows INF 文件或自定义的第三方 INF 文件。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon drivernodes *
devcon drivernodes *miniport*
devcon drivernodes =usb pci* usb*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例10：按硬件 ID 模式列出驱动程序包](devcon-examples.md#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[示例11：按设备实例 ID 模式列出驱动程序包](devcon-examples.md#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)
