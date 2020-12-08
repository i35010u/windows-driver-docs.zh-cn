---
title: promptIfDriverIsNotBetter XML 元素
description: promptIfDriverIsNotBetter XML 元素
keywords:
- promptIfDriverIsNotBetter XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- promptIfDriverIsNotBetter XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b5e30631444b7e394097079777c6746e3cedc87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796037"
---
# <a name="promptifdriverisnotbetter-xml-element"></a>promptIfDriverIsNotBetter XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**PromptIfDriverIsNotBetter** XML 元素是一个空元素，该元素将 **promptIfDriverIsNotBetter** 标志设置为 ON，这会将 DPInst 配置为在新驱动程序比设备上当前安装的驱动程序不能比设备更好地匹配时显示对话框。 此对话框通知用户这种情况，并提供一个选项，用于将设备上当前安装的驱动程序替换为新的驱动程序。

### <a name="element-tag"></a>元素标记

```cpp
<promptIfDriverIsNotBetter>
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

默认情况下， **promptIfDriverIsNotBetter** 标志设置为 OFF。 可以通过在 *DPInst.xml* 文件中包含 **promptIfDriverIsNotBetter** XML 元素或使用 **/P** 命令行开关将 **promptIfDriverIsNotBetter** 标志设置为 ON。

下面的代码示例演示了 **promptIfDriverIsNotBetter** 元素。

```cpp
<dpinst>
  ...
  <promptIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

