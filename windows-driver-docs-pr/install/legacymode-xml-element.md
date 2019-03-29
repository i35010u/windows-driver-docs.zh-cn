---
title: legacyMode XML 元素
description: LegacyMode XML 元素是空元素，用于 legacyMode 标志设置为 ON，将配置 DPInst 安装未签名驱动程序和缺少的文件的驱动程序包。
ms.assetid: a070551c-6053-42ba-873c-ac624afecfd0
keywords:
- legacyMode XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- legacyMode XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03a8bfe19b6ce5e545c6b2b8a17e540e85c6d235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563789"
---
# <a name="legacymode-xml-element"></a>legacyMode XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**LegacyMode** XML 元素为空元素，用于设置**legacyMode**标志为 ON，将配置 DPInst 安装未签名驱动程序并[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，具有缺少的文件。

**元素标记**

```cpp
<legacyMode>
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

 

**注释**

默认情况下，DPInst 安装仅签名[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)和不具有缺少的文件的驱动程序包。 若要配置 DPInst 接受未签名的驱动程序包或缺少文件的驱动程序包，请设置**legacyMode**通过包括标志为 ON **legacyMode**元素作为子元素的**dpinst** XML 元素或通过使用 **/lm** 命令行开关。

下面的代码示例演示**legacyMode**元素。

```cpp
<dpinst>
  ...
  <legacyMode/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






