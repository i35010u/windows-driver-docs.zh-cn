---
title: package XML 元素
description: 包 XML 元素指定的驱动程序包的 INF 文件。元素标记包 XML AttributespathThe INF 文件路径的驱动程序包。
ms.assetid: c7089e58-50c7-46ec-a9bf-c8e2d2bd354a
keywords:
- 包的 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- package XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9e3963531b94ed23490d0897cf98b72e0137f39c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363343"
---
# <a name="package-xml-element"></a>package XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**包**XML 元素指定用于的 INF 文件[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)。

**元素标记**

```cpp
<package>
```

**XML 特性**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>路径</strong></p></td>
<td align="left"><p>驱动程序包 INF 文件的路径。 该路径是相对于 DPInst 工作目录。</p></td>
</tr>
</tbody>
</table>

 

**元素的信息**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>父元素</strong></p></td>
<td align="left"><p><a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>group</strong></a></p></td>
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

 

**注释**

下面的代码示例演示**包**元素，它指定 DirAbc\\为的 INF 文件 Abc.inf[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" />
  </group>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**group**](group-xml-element.md)

 

 






