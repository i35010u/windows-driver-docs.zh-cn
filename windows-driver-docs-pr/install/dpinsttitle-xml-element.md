---
title: dpinstTitle XML 元素
description: dpinstTitle XML 元素
ms.assetid: a6867874-436b-414f-9610-aea585822a91
keywords:
- dpinstTitle XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- dpinstTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a6aae762e5d4d3e141ad2999940df64763b1248d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356047"
---
# <a name="dpinsttitle-xml-element"></a>dpinstTitle XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**DpinstTitle** XML 元素自定义的所有 DPInst 向导页面的标题栏显示的文本。

### <a name="element-tag"></a>元素标记

```cpp
<dpinstTitle>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>language</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>自定义所有向导页上的标题栏文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例的**dpinstTitle**元素自定义标题栏文本。 指定自定义的 DPInst 标题的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <dpinstTitle>Toaster Device Installer</dpinstTitle>
    ...
  </language>
  ...
</dpinst>
```

如果**dpinstTitle**元素未指定，DPInst 显示默认的欢迎页上显示的默认标题栏文本。

## <a name="see-also"></a>请参阅


[**language**](language-xml-element.md)

 

 






