---
title: subDirectory XML 元素
description: subDirectory XML 元素
ms.assetid: 41f86668-148e-4d7c-89b8-e3c21efffd7b
keywords:
- 子目录 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- subDirectory XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00a729317a484965cdc19926b2e61aa62a49b841
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385880"
---
# <a name="subdirectory-xml-element"></a>subDirectory XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**子目录**XML 元素指定 DPInst 工作目录下的一个或所有的子目录。

### <a name="element-tag"></a>元素标记

```cpp
<subDirectory>
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
<td align="left"><p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>search</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>指定一个或全部是相对于 DPInst 工作目录的子目录。 此元素可以包含：</p>
<ul>
<li><p>指定特定的子目录的字符串</p></li>
<li><p>通配符字符 (<strong>*</strong>) 指定的所有子目录</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**搜索**元素，其中包含一个**子目录**指定的元素*i386* DPInst 工作下的子目录目录。 指定自定义的子目录的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

下面的代码示例演示**搜索**元素，其中包含**子目录**指定 DPInst 工作目录下的子目录中的所有元素。 通配符字符 (\*)，它指定的所有子目录中粗体的字体样式显示。

```cpp
<search>
  <subDirectory>*</subDirectory>
</search>
```

## <a name="see-also"></a>请参阅


[**search**](search-xml-element.md)

 

 






