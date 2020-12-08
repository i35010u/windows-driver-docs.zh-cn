---
title: legacyMode XML 元素
description: LegacyMode XML 元素是一个空元素，用于将 legacyMode 标志设置为 ON，后者配置 DPInst 以安装未签名的驱动程序和包含缺少文件的驱动程序包。
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
ms.openlocfilehash: ae0519da745e932f47305d412d885e88ce01bba4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818893"
---
# <a name="legacymode-xml-element"></a>legacyMode XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**LegacyMode** XML 元素是一个空元素，用于将 **legacyMode** 标志设置为 ON，后者配置 DPInst 以安装未签名的驱动程序和包含缺少文件的 [驱动程序包](./driver-packages.md)。

**元素标记**

```cpp
<legacyMode>
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
<td align="left"><p>不允许</p></td>
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

 

**备注**

默认情况下，DPInst 仅安装已签名的 [驱动程序包](./driver-packages.md) 和不缺少文件的驱动程序包。 若要配置 DPInst 以接受未签名的驱动程序包或包含缺少文件的驱动程序包，请将 **legacyMode** 元素包含为 **DPInst** XML 元素的子元素或使用 **/lm** 命令行开关，将 **legacyMode** 标志设置为 ON。

下面的代码示例演示了 **legacyMode** 元素。

```cpp
<dpinst>
  ...
  <legacyMode/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

