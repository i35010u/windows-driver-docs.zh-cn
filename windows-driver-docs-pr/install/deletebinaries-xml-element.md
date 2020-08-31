---
title: deleteBinaries XML 元素
description: DeleteBinaries XML 元素是一个空元素，该元素将 deleteBinaries 标志设置为 ON，后者将配置 DPInst，以删除系统中的二进制文件，这些文件是在安装驱动程序包时复制到系统的。元素标记 deleteBinaries XML AttributesNoneElement Information Parent elementsdpinstChild elementsNoneData contentsNone permittedDuplicate child elementsNone 允许 RemarksBy 默认情况下，deleteBinaries 标志设置为 OFF。 若要将 deleteBinaries 标志设置为 ON，请将 deleteBinaries 元素包含为 dpinst 元素的子元素，或使用/d DPInst 命令行开关。 下面的代码示例演示了 deleteBinaries 元素。 dpinst .。。deleteBinaries/.../dpinst 注意从 Windows 7 开始，操作系统会忽略 deleteBinaries XML 元素的的设置。 安装驱动程序包后，将无法再使用 DPInst 删除已复制到系统中的二进制文件。
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
ms.openlocfilehash: f05694ba3c63601aa0df5327c51632c0857e3109
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096303"
---
# <a name="deletebinaries-xml-element"></a>deleteBinaries XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**DeleteBinaries** XML 元素是一个空元素，该元素将**deleteBinaries**标志设置为 ON，后者将配置 DPInst，以删除系统中的二进制文件，这些文件是在安装[驱动程序包](./driver-packages.md)时复制到系统的。

**元素标记**

```cpp
<deleteBinaries>
```

**XML 特性**

无

**元素信息**

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
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

**注释**

默认情况下， **deleteBinaries** 标志设置为 OFF。 若要将**deleteBinaries**标志设置为 ON，请将**deleteBinaries**元素包含为**dpinst**元素的子元素，或使用 **/d**   dpinst 命令行开关。

下面的代码示例演示了 **deleteBinaries** 元素。

```cpp
<dpinst>
  ...
   <deleteBinaries/>
  ...
</dpinst>
```

**注意**   从 Windows 7 开始，操作系统会忽略**deleteBinaries** XML 元素的的设置。 安装 [驱动程序包](./driver-packages.md) 后，将无法再使用 DPInst 删除已复制到系统中的二进制文件。

 

## <a name="see-also"></a>另请参阅


[**dpinst**](dpinst-xml-element.md)

 

