---
title: search XML 元素
description: search XML 元素
ms.assetid: 34eff240-a96a-4b73-a001-5ea698e9f7ae
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
ms.openlocfilehash: 397fba7639374dcad7a28f22a44528674db45c62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348695"
---
# <a name="search-xml-element"></a>search XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**搜索**XML 元素将定向 DPInst INF 文件往复搜索指定 DPInst 工作目录下的子目录中。 由一个或多个指定子目录[**子目录子元素**](subdirectory-xml-element.md)。

### <a name="element-tag"></a>元素标记

```cpp
<search>
```

### <a name="xml-attributes"></a>XML 特性

无

### <a name="element-information"></a>**元素的信息**

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
<td align="left"><p><a href="subdirectory-xml-element.md" data-raw-source="[&lt;strong&gt;subDirectory&lt;/strong&gt;](subdirectory-xml-element.md)"><strong>子目录</strong></a> （零个或多个）</p></td>
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

下面的代码示例演示**搜索**元素，其中包含一个**子目录**指定的 XML 元素*i386*子目录。 DPInst 将以递归方式搜索[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)中*i386* DPInst 工作目录的子目录。 指定自定义的子目录的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

**请注意**  因为重复的子元素不允许使用，每个**子目录**的子元素**搜索**元素必须是唯一的。

 

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**subDirectory**](subdirectory-xml-element.md)

 

 






