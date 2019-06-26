---
title: dpinst XML 元素
description: dpinst XML 元素
ms.assetid: d825afb4-a459-4b69-93cb-db57adab3c80
keywords:
- dpinst XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- dpinst XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fb1580b7fad983a81560716ed3e3ad4bf89cb1d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375300"
---
# <a name="dpinst-xml-element"></a>dpinst XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**Dpinst** XML 元素是包含自定义驱动程序安装的子元素的 DPInst 描述符文件中的根 XML 元素。

### <a name="element-tag"></a>元素标记

```cpp
<dpinst>
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
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p><a href="enablenotlistedlanguages-xml-element.md" data-raw-source="[&lt;strong&gt;enableNotListedLanguages&lt;/strong&gt;](enablenotlistedlanguages-xml-element.md)"><strong>enableNotListedLanguages</strong> </a> （零个或一个）</p>
<p><a href="deletebinaries-xml-element.md" data-raw-source="[&lt;strong&gt;deleteBinaries&lt;/strong&gt;](deletebinaries-xml-element.md)"><strong>deleteBinaries</strong> </a> （零个或一个）</p>
<p><a href="forceifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;forceIfDriverIsNotBetter&lt;/strong&gt;](forceifdriverisnotbetter-xml-element.md)"><strong>forceIfDriverIsNotBetter</strong> </a> （零个或一个）</p>
<p><a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>组</strong></a> （零个或多个）</p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong> </a> （零个或一个）</p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>图标</strong></a> （零个或一个）</p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong> </a> （零个或一个）</p>
<p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a> （零个或多个）</p>
<p><a href="legacymode-xml-element.md" data-raw-source="[&lt;strong&gt;legacyMode&lt;/strong&gt;](legacymode-xml-element.md)"><strong>legacyMode</strong> </a> （零个或一个）</p>
<p><a href="promptifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;promptIfDriverIsNotBetter&lt;/strong&gt;](promptifdriverisnotbetter-xml-element.md)"><strong>promptIfDriverIsNotBetter</strong> </a> （零个或一个）</p>
<p><a href="quietinstall-xml-element.md" data-raw-source="[&lt;strong&gt;quietInstall&lt;/strong&gt;](quietinstall-xml-element.md)"><strong>quietInstall</strong> </a> （零个或一个）</p>
<p><a href="scanhardware-xml-element.md" data-raw-source="[&lt;strong&gt;scanHardware&lt;/strong&gt;](scanhardware-xml-element.md)"><strong>scanHardware</strong> </a> （零个或一个）</p>
<p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>搜索</strong></a> （零个或多个）</p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong> </a> （零个或一个）</p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong> </a> （零个或一个）</p></td>
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

下面的代码示例演示了 XML 声明的元素后, 跟**dpinst**元素，它包含零个或多个子元素。

```cpp
<?xml version="1.0" ?>
<dpinst>
  ...
</dpinst>
```

**请注意**  因为重复的子元素不允许使用，每个**搜索**子元素和**语言**元素**dpinst**元素必须是唯一的。

 

## <a name="see-also"></a>请参阅


[**deleteBinaries**](deletebinaries-xml-element.md)

[**enableNotListedLanguages**](enablenotlistedlanguages-xml-element.md)

[**forceIfDriverIsNotBetter**](forceifdriverisnotbetter-xml-element.md)

[**group**](group-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**icon**](icon-xml-element.md)

[**installAllOrNone**](installallornone-xml-element.md)

[**language**](language-xml-element.md)

[**legacyMode**](legacymode-xml-element.md)

[**promptIfDriverIsNotBetter**](promptifdriverisnotbetter-xml-element.md)

[**quietInstall**](quietinstall-xml-element.md)

[**scanHardware**](scanhardware-xml-element.md)

[**search**](search-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

 

 






