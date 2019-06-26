---
title: promptIfDriverIsNotBetter XML 元素
description: promptIfDriverIsNotBetter XML 元素
ms.assetid: e5808c64-daa8-4aad-9a63-7ff79b0c2e49
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
ms.openlocfilehash: 0a9c6d95db60d5cce48b0c27013bf199a58e249f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380469"
---
# <a name="promptifdriverisnotbetter-xml-element"></a>promptIfDriverIsNotBetter XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**PromptIfDriverIsNotBetter** XML 元素为空元素，用于设置**promptIfDriverIsNotBetter**标志为 ON，将配置 DPInst 以显示一个对话框中，如果新的驱动程序不是更好的匹配项到比当前安装在设备的驱动程序的设备。 对话框告知用户这种情况下的，并提供了一个选项以替换与新的驱动程序在设备当前安装的驱动程序。

### <a name="element-tag"></a>元素标记

```cpp
<promptIfDriverIsNotBetter>
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

默认情况下**promptIfDriverIsNotBetter**标志设置为 OFF。 可以设置**promptIfDriverIsNotBetter**通过包括标志为 ON **promptIfDriverIsNotBetter**中的 XML 元素*DPInst.xml*文件或通过使用 **/ p** 命令行开关。

下面的代码示例演示**promptIfDriverIsNotBetter**元素。

```cpp
<dpinst>
  ...
  <promptIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






