---
title: search XML 元素
description: search XML 元素
keywords:
- 搜索 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- search XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71896dfee120a14a1432db9da0b642457d44b3ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834501"
---
# <a name="search-xml-element"></a>search XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Search** XML 元素指示 DPInst 在 DPInst 工作目录下的指定子目录中以递归方式搜索 INF 文件。 子目录由一个或多个 [**子目录子元素**](subdirectory-xml-element.md)指定。

### <a name="element-tag"></a>元素标记

```cpp
<search>
```

### <a name="xml-attributes"></a>XML 属性

无

### <a name="element-information"></a>**元素信息**

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
<td align="left"><p><a href="subdirectory-xml-element.md" data-raw-source="[&lt;strong&gt;subDirectory&lt;/strong&gt;](subdirectory-xml-element.md)"><strong>子目录</strong></a> (零个或多个) </p></td>
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

下面的代码示例演示一个 **搜索** 元素，该元素包含一个指定 *I386* 子目录的 **子目录** XML 元素。 DPInst 将以递归方式在 DPInst 工作目录的 *i386* 子目录中搜索 [驱动程序包](./driver-packages.md)。 指定自定义子目录的文本以粗体显示。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

**注意** 由于不允许使用重复的子元素，因此 **搜索** 元素 **的每个子元素都必须** 是唯一的。

 

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**光标**](subdirectory-xml-element.md)

 

