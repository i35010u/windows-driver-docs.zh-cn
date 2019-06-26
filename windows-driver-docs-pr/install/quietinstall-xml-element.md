---
title: quietInstall XML 元素
description: quietInstall XML 元素
ms.assetid: 1151a68f-17c8-4852-9dc0-ab5dea9d58c6
keywords:
- quietInstall XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- quietInstall XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c26850c3949f9cc69d7cf55ab2b51b2f6bf990c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386401"
---
# <a name="quietinstall-xml-element"></a>quietInstall XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**QuietInstall** XML 元素为空元素，用于设置**quietInstall**标志为 ON，将配置 DPInst 禁止显示的向导页和大多数其他用户消息。

### <a name="element-tag"></a>**元素标记**

```cpp
<quietInstall>
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

默认情况下**quietInstall**标志设置为 OFF。 可以设置**quietInstall**通过包括标志为 ON **quietInstall**元素 DPInst 描述符文件中或通过使用 **/q** 命令行开关。 **QuietInstall**标志适用于的 EULA 页面是否存在并**suppressEulaPage**标志。

下面的代码示例演示**quietInstall**元素

```cpp
<dpinst>
  ...
  <quietInstall/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






