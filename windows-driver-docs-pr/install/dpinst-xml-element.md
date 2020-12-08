---
title: dpinst XML 元素
description: dpinst XML 元素
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
ms.openlocfilehash: dd080e91b1f93d67bbfd1999449d51545515501b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782743"
---
# <a name="dpinst-xml-element"></a>dpinst XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Dpinst** XML 元素是 dpinst 描述符文件中的根 xml 元素，该元素包含自定义驱动程序安装的子元素。

### <a name="element-tag"></a>元素标记

```cpp
<dpinst>
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
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p><a href="enablenotlistedlanguages-xml-element.md" data-raw-source="[&lt;strong&gt;enableNotListedLanguages&lt;/strong&gt;](enablenotlistedlanguages-xml-element.md)"><strong>enableNotListedLanguages</strong></a> (零个或一个) </p>
<p><a href="deletebinaries-xml-element.md" data-raw-source="[&lt;strong&gt;deleteBinaries&lt;/strong&gt;](deletebinaries-xml-element.md)"><strong>deleteBinaries</strong></a> (零个或一个) </p>
<p><a href="forceifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;forceIfDriverIsNotBetter&lt;/strong&gt;](forceifdriverisnotbetter-xml-element.md)"><strong>forceIfDriverIsNotBetter</strong></a> (零个或一个) </p>
<p><a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>组</strong></a> (零个或多个) </p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong></a> (零个或一个) </p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>图标</strong></a> (零个或一个) </p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong></a> (零个或一个) </p>
<p> (零个或多个<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a>) </p>
<p><a href="legacymode-xml-element.md" data-raw-source="[&lt;strong&gt;legacyMode&lt;/strong&gt;](legacymode-xml-element.md)"><strong>legacyMode</strong></a> (零个或一个) </p>
<p><a href="promptifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;promptIfDriverIsNotBetter&lt;/strong&gt;](promptifdriverisnotbetter-xml-element.md)"><strong>promptIfDriverIsNotBetter</strong></a> (零个或一个) </p>
<p><a href="quietinstall-xml-element.md" data-raw-source="[&lt;strong&gt;quietInstall&lt;/strong&gt;](quietinstall-xml-element.md)"><strong>quietInstall</strong></a> (零个或一个) </p>
<p><a href="scanhardware-xml-element.md" data-raw-source="[&lt;strong&gt;scanHardware&lt;/strong&gt;](scanhardware-xml-element.md)"><strong>scanHardware</strong></a> (零个或一个) </p>
<p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>搜索</strong></a> (零个或多个) </p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong></a> (零个或一个) </p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong></a> (零个或一个) </p></td>
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

下面的代码示例演示一个 XML 声明元素，后跟一个包含零个或多个子元素的 **dpinst** 元素。

```cpp
<?xml version="1.0" ?>
<dpinst>
  ...
</dpinst>
```

**注意** 由于不允许使用重复的子元素，因此 **dpinst** 元素的每个 **搜索** 子元素和 **language** 元素都必须是唯一的。

 

## <a name="see-also"></a>请参阅


[**deleteBinaries**](deletebinaries-xml-element.md)

[**enableNotListedLanguages**](enablenotlistedlanguages-xml-element.md)

[**forceIfDriverIsNotBetter**](forceifdriverisnotbetter-xml-element.md)

[**组**](group-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**按钮**](icon-xml-element.md)

[**installAllOrNone**](installallornone-xml-element.md)

[**语言**](language-xml-element.md)

[**legacyMode**](legacymode-xml-element.md)

[**promptIfDriverIsNotBetter**](promptifdriverisnotbetter-xml-element.md)

[**quietInstall**](quietinstall-xml-element.md)

[**scanHardware**](scanhardware-xml-element.md)

[**寻找**](search-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

 

