---
title: group XML 元素
description: group XML 元素
ms.assetid: 8035fd60-065c-4282-a18c-34e6a5201e56
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
ms.openlocfilehash: 67ad637c336cb3e85113b6d55d3517d01dfb9257
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387336"
---
# <a name="group-xml-element"></a>group XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**组**XML 元素指定的有序的集合[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)该 DPInst 处理作为驱动程序包组。

### <a name="element-tag"></a>元素标记

```cpp
<group>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p><a href="package-xml-element.md" data-raw-source="[&lt;strong&gt;package&lt;/strong&gt;](package-xml-element.md)"><strong>包</strong></a> （零个或多个）</p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong> </a> （零个或一个）</p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong> </a> （零个或一个）</p></td>
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

下面的代码示例演示**组**元素包含两个[**打包 XML 元素**](package-xml-element.md)并[ **installAllOrNoneXML 元素**](installallornone-xml-element.md)。 该示例**组**元素配置来处理"Abc"的 DPInst[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)和"Def"驱动程序包作为一个组。 **InstallAllOrNone** XML 元素配置 DPInst 安装驱动程序程序包组中的驱动程序包，才可以安装这两个驱动程序。

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

[**package**](package-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

 

 






