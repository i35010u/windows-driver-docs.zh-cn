---
title: forceIfDriverIsNotBetter XML 元素
description: forceIfDriverIsNotBetter XML 元素
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
ms.openlocfilehash: 638c76b962b2c25b0340688ad984ef0b8db31d0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820187"
---
# <a name="forceifdriverisnotbetter-xml-element"></a>forceIfDriverIsNotBetter XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**ForceIfDriverIsNotBetter** XML 元素是一个空元素，用于将 **forceIfDriverIsNotBetter** 标志设置为 ON，这会将 DPInst 配置为在设备上安装驱动程序，即使当前安装在设备上的驱动程序比新驱动程序更匹配。

### <a name="element-tag"></a>元素标记

```cpp
<forceIfDriverIsNotBetter>
```

### <a name="xml-attributes"></a>XML 属性

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
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

默认情况下， **forceIfDriverIsNotBetter** 标志设置为 OFF。 您可以通过将 **forceIfDriverIsNotBetter** 元素包含为 dpinst 描述符文件中 [**dpinst XML 元素**](dpinst-xml-element.md)的子元素或使用 **/f** 命令行开关，将 **forceIfDriverIsNotBetter** 标志设置为 ON。

下面的代码示例演示了 **forceIfDriverIsNotBetter** 元素。

```cpp
<dpinst>
  ...
  <forceIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

