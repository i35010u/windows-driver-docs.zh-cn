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
ms.openlocfilehash: 26ac21a7d8b1b9db9aef1c8c957a8f6f1c43387e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339638"
---
# <a name="suppressaddremoveprograms-xml-element"></a>suppressAddRemovePrograms XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**SuppressAddRemovePrograms** XML 元素为空元素，用于设置**suppressAddRemovePrograms**标志为 ON，将配置 DPInst 若要禁止显示的项添加**程序和功能**控制面板中。 这些条目都代表[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)和 DPInst 安装驱动程序包组。

**请注意**  在版本的 Windows 早于 Windows Vista，DPInst 添加到驱动程序包的条目**添加或删除程序**控制面板中。

 

### <a name="element-tag"></a>元素标记

```cpp
<suppressAddRemovePrograms>
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

默认情况下**suppressAddRemovePrograms**标志设置为 OFF。 若要设置**suppressAddRemovePrograms**为开 DPInst 安装，包括所有驱动程序中的驱动程序的所有标志[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)组，包括**suppressAddRemovePrograms**元素的子元素作为**dpinst** DPInst 描述符文件中或使用中的 XML 元素 **/sa** 命令行开关。 若要设置**suppressAddRemoverPrograms**标志仅对特定的驱动程序包组的包括**suppressAddRemovePrograms**作为子元素的相应元素**组** DPInst 描述符文件中的 XML 元素。

下面的代码示例演示**suppressAddRemovePrograms**是子元素的元素**dpinst**元素。

```cpp
<dpinst>
  ...
   <suppressAddRemovePrograms/>
  ...
</dpinst>
```

下面的代码示例演示**suppressAddRemovePrograms**是子元素的元素**组**元素。

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

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**group**](group-xml-element.md)

 

 






