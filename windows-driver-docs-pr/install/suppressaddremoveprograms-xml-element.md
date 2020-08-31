---
title: suppressAddRemovePrograms XML 元素
description: suppressAddRemovePrograms XML 元素
ms.assetid: ab3bac90-dffa-400b-916a-a7deecbc42d7
keywords:
- suppressAddRemovePrograms XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- suppressAddRemovePrograms XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 300e6eb68587934e202f30dd2fe0a38288ce9a92
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094849"
---
# <a name="suppressaddremoveprograms-xml-element"></a>suppressAddRemovePrograms XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**SuppressAddRemovePrograms** XML 元素是一个空元素，该元素将**suppressAddRemovePrograms**标志设置为 ON，这会将 DPInst 配置为禁止将条目添加到控制面板中的 "**程序和功能**"。 这些条目表示 DPInst 安装的 [驱动程序包](./driver-packages.md) 和驱动程序包组。

**注意**   在早于 Windows Vista 的 Windows 版本中，DPInst 将驱动程序包条目添加到控制面板中的 "**添加或删除程序**"。

 

### <a name="element-tag"></a>元素标记

```cpp
<suppressAddRemovePrograms>
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

默认情况下， **suppressAddRemovePrograms** 标志设置为 OFF。 若要为 DPInst 安装的所有驱动程序（包括[驱动程序包](./driver-packages.md)组中的所有驱动程序）将**suppressAddRemovePrograms**标志设置为 ON，请在 DPInst 描述符文件中包含**suppressAddRemovePrograms**元素作为**DPInst** XML 元素的子元素，或使用 **/sa**   命令行开关。 若要仅为特定驱动程序包组设置**suppressAddRemoverPrograms**标志，请在 DPInst 描述符文件中的相应**组**XML 元素的子元素中包括**suppressAddRemovePrograms**元素。

下面的代码示例演示了作为**dpinst**元素的子元素的**suppressAddRemovePrograms**元素。

```cpp
<dpinst>
  ...
   <suppressAddRemovePrograms/>
  ...
</dpinst>
```

下面的代码示例演示一个作为**group**元素的子元素的**suppressAddRemovePrograms**元素。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" /> 
    <package path="DirDef\Def.inf" /> 
    <suppressAddRemovePrograms/>
  <group/>
  ...
</dpinst>
```

## <a name="see-also"></a>另请参阅


[**dpinst**](dpinst-xml-element.md)

[**group**](group-xml-element.md)

 

