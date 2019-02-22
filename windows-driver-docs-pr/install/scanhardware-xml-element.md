---
title: scanHardware XML 元素
description: scanHardware XML 元素
ms.assetid: c1af7238-97e9-4c5f-95ea-fbc9f3cc8279
keywords:
- scanHardware XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- scanHardware XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: afe2572d2241d694e64d9ad860a2a5a85c7060b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533144"
---
# <a name="scanhardware-xml-element"></a>scanHardware XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**ScanHardware** XML 元素为空元素，用于设置**scanHardware**标志为 ON。 将此标志设置为 ON 配置 DPInst 安装[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)插即用 (PnP) 函数驱动程序仅当驱动程序包与匹配的计算机中配置的设备和驱动程序包是一个更适合的比当前安装在设备的驱动程序包的设备。

### <a name="element-tag"></a>元素标记

```cpp
<scanHardware>
```

### <a name="xml-attributes"></a>XML 特性

无

### <a name="element-information"></a>元素信息

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>父元素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

默认情况下**scanHardware**标志设置为 OFF。 可以设置**scanHardware**通过包括标志为 ON **scanHardware**作为子元素的 XML 元素**dpinst** DPInst 描述符文件中或通过使用 XML 元素 **/sh** 命令行开关。

下面的代码示例演示**scanHardware**元素。

```cpp
<dpinst>
  ...
  <scanHardware/>
  ...
</dpinst>
```

 

 





