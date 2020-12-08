---
title: subDirectory XML 元素
description: subDirectory XML 元素
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
ms.openlocfilehash: 1b253b7337d1cb2295172fcf832d78d3e3fd916a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820701"
---
# <a name="subdirectory-xml-element"></a>subDirectory XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**子目录** XML 元素指定 DPInst 工作目录下的一个或所有子目录。

### <a name="element-tag"></a>元素标记

```cpp
<subDirectory>
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
<td align="left"><p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>寻找</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>指定相对于 DPInst 工作目录的一个或所有子目录。 此元素可以包含：</p>
<ul>
<li><p>用于指定特定子目录的字符串</p></li>
<li><p>通配符 (<strong>*</strong>) 指定所有子目录</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示一个 **搜索** 元素，该元素包含一个 **子目录** 元素，该元素指定 DPInst 工作目录下的 *i386* 子目录。 指定自定义子目录的文本以粗体显示。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

下面的代码示例演示一个 **搜索** 元素，该元素包含一个 **子目录** 元素，该元素指定 DPInst 工作目录下的所有子目录。 \*用于指定所有子目录的通配符 () 以粗体显示。

```cpp
<search>
  <subDirectory>*</subDirectory>
</search>
```

## <a name="see-also"></a>请参阅


[**寻找**](search-xml-element.md)

 

