---
title: group XML 元素
description: group XML 元素
keywords:
- 组 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- group XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 59af6763d4d756c43bb0cd2d64bd51efb94ddb27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791465"
---
# <a name="group-xml-element"></a>group XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**组** XML 元素指定 DPInst 处理为驱动程序包组的 [驱动程序包](./driver-packages.md)的有序集合。

### <a name="element-tag"></a>元素标记

```cpp
<group>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p><a href="package-xml-element.md" data-raw-source="[&lt;strong&gt;package&lt;/strong&gt;](package-xml-element.md)"><strong>包</strong></a> (零个或多个) </p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong></a> (零个或一个) </p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong></a> (零个或一个) </p></td>
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

下面的代码示例演示了一个 **组** 元素，其中包含两个 [**package xml 元素**](package-xml-element.md) 和一个 [**installAllOrNone xml 元素**](installallornone-xml-element.md)。 示例 **group** 元素将 DPInst 配置为以组的形式处理 "Abc" [驱动程序包](./driver-packages.md) 和 "Def" 驱动程序包。 **InstallAllOrNone** XML 元素将 DPInst 配置为仅在可以安装两个驱动程序时才将驱动程序包安装到驱动程序包组。

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

[**installAllOrNone**](installallornone-xml-element.md)

[**软件包**](package-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

 

