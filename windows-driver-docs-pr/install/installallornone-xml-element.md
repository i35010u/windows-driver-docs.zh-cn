---
title: installAllOrNone XML 元素
description: installAllOrNone XML 元素
ms.assetid: f5634def-c9a1-45db-88ce-f652171d19c9
keywords:
- installAllOrNone XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- installAllOrNone XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8d9f8f43c33da258a35f2831d2a30207b2570ea1
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095499"
---
# <a name="installallornone-xml-element"></a>installAllOrNone XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**InstallAllOrNone** XML 元素是一个空元素，该元素将**installAllOrNone**标志设置为 ON，这会将 DPInst 配置为仅当安装包中的所有驱动程序包都可安装时，或者如果驱动程序包组中的所有驱动程序包都可以安装，才将配置为在[驱动程序包](./driver-packages.md)中安装驱动程序。

### <a name="element-tag"></a>**元素标记**

```cpp
<installAllOrNone>
```

### <a name="xml-attributes"></a>**XML 特性**

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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a>或<a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"> <strong>group</strong></a></p></td>
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

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

默认情况下， **installAllOrNone** 标志设置为 OFF。 若要为所有驱动程序包（包括驱动程序包组中的[驱动程序包](./driver-packages.md)）将**installAllOrNone**标志设置为 ON，请将**installAllOrNone**元素包含为**dpinst** XML 元素的子元素，或使用 **/a**   命令行开关。 若要将 **installAllOrNone** 标志设置为仅对特定驱动程序包组启用，请将 **installAllOrNone** 元素包含为相应 **组** XML 元素的子元素。

下面的代码示例演示作为**dpinst**元素的子元素的**installAllOrNone**元素。

```cpp
<dpinst>
  ...
  <installAllOrNone/>
  ...
</dpinst>
```

下面的代码示例演示一个作为**group**元素的子元素的**installAllOrNone**元素。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" /> 
    <package path="DirDef\Def.inf" /> 
    <installAllOrNone/>
  <group/>
  ...
</dpinst>
```

## <a name="see-also"></a>另请参阅


[**dpinst**](dpinst-xml-element.md)

[**group**](group-xml-element.md)

 

