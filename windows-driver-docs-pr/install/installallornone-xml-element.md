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
ms.openlocfilehash: 9a3bc72cbccd803c0adb5f3d37026f2853ac6340
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325802"
---
# <a name="installallornone-xml-element"></a>installAllOrNone XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**InstallAllOrNone** XML 元素为空元素，用于设置**installAllOrNone**为开，这会将配置 DPInst 安装驱动程序中的标志[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)仅如果在安装包中的驱动程序包可以安装，或可以安装所有驱动程序程序包组中的驱动程序包。

### <a name="element-tag"></a>**元素标记**

```cpp
<installAllOrNone>
```

### <a name="xml-attributes"></a>**XML 特性**

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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>或<a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>组</strong></a></p></td>
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

 

### <a href="" id="comments"></a>备注

默认情况下**installAllOrNone**标志设置为 OFF。 若要设置**installAllOrNone**为开的所有标志[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，包括中的包的驱动程序组，包括**installAllOrNone**子元素元素**dpinst** XML 元素，或使用 **/a** 命令行开关。 若要设置**installAllOrNone**标记为特定的驱动程序包组仅可为 ON，包括**installAllOrNone**作为子元素的相应元素**组**XML 元素。

下面的代码示例演示**installAllOrNone**元素的子元素**dpinst**元素。

```cpp
<dpinst>
  ...
  <installAllOrNone/>
  ...
</dpinst>
```

下面的代码示例演示**installAllOrNone**元素的子元素**组**元素。

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

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**group**](group-xml-element.md)

 

 






