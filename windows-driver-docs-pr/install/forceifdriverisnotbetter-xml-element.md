---
title: forceIfDriverIsNotBetter XML 元素
description: forceIfDriverIsNotBetter XML 元素
ms.assetid: ba83c8fd-cc8e-44fd-96ed-855bb42c2493
keywords:
- forceIfDriverIsNotBetter XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- forceIfDriverIsNotBetter XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6ffb8aea9579a7d0fde2fc948528a73745c3086c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353794"
---
# <a name="forceifdriverisnotbetter-xml-element"></a>forceIfDriverIsNotBetter XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**ForceIfDriverIsNotBetter** XML 元素为空元素，用于设置**forceIfDriverIsNotBetter**标志为 ON，将配置 DPInst 安装在设备上的驱动程序，即使这是驱动程序在设备上当前安装的是更好的匹配比新的驱动程序。

### <a name="element-tag"></a>元素标记

```cpp
<forceIfDriverIsNotBetter>
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

默认情况下**forceIfDriverIsNotBetter**标志设置为 OFF。 可以设置**forceIfDriverIsNotBetter**通过包括标志为 ON **forceIfDriverIsNotBetter**作为子元素的元素[ **dpinst XML 元素**](dpinst-xml-element.md) DPinst 描述符文件中或通过使用 **/f**命令行开关。

下面的代码示例演示**forceIfDriverIsNotBetter**元素。

```cpp
<dpinst>
  ...
  <forceIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






