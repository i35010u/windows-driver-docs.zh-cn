---
title: deleteBinaries XML 元素
description: DeleteBinaries XML 元素是空元素，用于 deleteBinaries 标志设置为 ON，将配置 DPInst 安装驱动程序包时复制到系统的系统从删除二进制文件。元素标记 deleteBinaries XML AttributesNoneElement 信息父 elementsdpinstChild elementsNoneData contentsNone permittedDuplicate 子 elementsNone 允许说明默认情况下，deleteBinaries 标志设置为 OFF。 若要将 deleteBinaries 标志设置为 ON，作为 dpinst 元素的子元素包括 deleteBinaries 元素，或使用 /d DPInst 命令行开关。 下面的代码示例演示 deleteBinaries 元素。 dpinst...deleteBinaries /.../ dpinst 注意从 Windows 7 中，操作系统会忽略为 deleteBinaries XML 元素设置为 ON。 当已安装驱动程序包时，不再可以通过使用 DPInst 删除已复制到系统二进制文件。
ms.assetid: 2711b2c2-b1ec-41cb-aeb2-1d9078740075
keywords:
- deleteBinaries XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- deleteBinaries XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bcee0636cb5c3141c812735c8c8cb4089044732e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565415"
---
# <a name="deletebinaries-xml-element"></a>deleteBinaries XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**DeleteBinaries** XML 元素为空元素，用于设置**deleteBinaries**标志为 ON，将配置从一个系统，已复制到系统时删除二进制文件的DPInst[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)已安装。

**元素标记**

```cpp
<deleteBinaries>
```

**XML 特性**

无

**元素的信息**

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
<td align="left"><p>无</p></td>
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

 

**注释**

默认情况下**deleteBinaries**标志设置为 OFF。 若要设置**deleteBinaries**标志为 ON，包括**deleteBinaries**作为子元素的元素**dpinst**元素或使用 **/d** DPInst 命令行开关。

下面的代码示例演示**deleteBinaries**元素。

```cpp
<dpinst>
  ...
   <deleteBinaries/>
  ...
</dpinst>
```

**请注意**  从 Windows 7 开始，操作系统会忽略设置为 ON **deleteBinaries** XML 元素。 已复制到系统的二进制文件时[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)已安装，不能再使用 DPInst 被删除。

 

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






