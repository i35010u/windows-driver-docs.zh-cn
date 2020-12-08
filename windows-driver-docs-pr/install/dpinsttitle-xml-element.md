---
title: dpinstTitle XML 元素
description: dpinstTitle XML 元素
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
ms.openlocfilehash: c1d193089e7a8243b0a3b3bf9e31f687d5f9655e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782737"
---
# <a name="dpinsttitle-xml-element"></a>dpinstTitle XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**DpinstTitle** XML 元素自定义显示在所有 DPInst 向导页面的标题栏中的文本。

### <a name="element-tag"></a>元素标记

```cpp
<dpinstTitle>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>自定义所有向导页上的标题栏文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例 **dpinstTitle** 元素自定义标题栏文本。 指定自定义 DPInst 标题的文本以粗体显示。

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

如果未指定 **dpinstTitle** 元素，则 DPInst 将显示默认的 "欢迎使用" 页上显示的默认标题栏文本。

## <a name="see-also"></a>请参阅


[**语言**](language-xml-element.md)

 

