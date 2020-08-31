---
title: package XML 元素
description: Package XML 元素为驱动程序包指定 INF 文件。元素标记包 XML AttributespathThe 驱动程序包的 INF 文件的路径。
ms.assetid: c7089e58-50c7-46ec-a9bf-c8e2d2bd354a
keywords:
- 包 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- package XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ab8fb9ac426da31f19220867b8071941a2379175
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095895"
---
# <a name="package-xml-element"></a>package XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Package** XML 元素为[驱动程序包](./driver-packages.md)指定 INF 文件。

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
<td align="left"><p>驱动程序包的 INF 文件的路径。 路径相对于 DPInst 工作目录。</p></td>
</tr>
</tbody>
</table>

 

**元素信息**

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
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

**注释**

下面的代码示例演示了一个 **package** 元素，该元素将 DirAbc \\ Abc 指定为 [驱动程序包](./driver-packages.md)的 inf 文件。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" />
  </group>
  ...
</dpinst>
```

## <a name="see-also"></a>另请参阅


[**group**](group-xml-element.md)

 

