---
title: language XML 元素
description: language XML 元素
ms.assetid: 1fc6a3b4-379e-4fd3-b526-c4193e9e84c5
keywords:
- 语言 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- language XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da8552175583d01ed9f7e6e7e67c0d3b18c14a50
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097327"
---
# <a name="language-xml-element"></a>language XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Language** XML 元素本地化和自定义 DPInst 在其向导页上显示的项。

### <a name="element-tag"></a>元素标记

```cpp
<language>
```

### <a name="xml-attributes"></a>XML 属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>代码</strong></p></td>
<td align="left"><p>十六进制格式或十进制格式的语言标识符。</p></td>
</tr>
</tbody>
</table>

 

### <a name="element-information"></a>**元素信息**

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
<td align="left"><p><a href="dpinsttitle-xml-element.md" data-raw-source="[&lt;strong&gt;dpinstTitle&lt;/strong&gt;](dpinsttitle-xml-element.md)"><strong>dpinstTitle</strong></a> (零个或一个) </p>
<p><a href="eula-xml-element.md" data-raw-source="[&lt;strong&gt;eula&lt;/strong&gt;](eula-xml-element.md)"><strong>eula</strong></a> (零个或一个) </p>
<p><a href="eulaheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;eulaHeaderTitle&lt;/strong&gt;](eulaheadertitle-xml-element.md)"><strong>eulaHeaderTitle</strong></a> (零个或一个) </p>
<p><a href="eulanobutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaNoButton&lt;/strong&gt;](eulanobutton-xml-element.md)"><strong>eulaNoButton</strong></a> (零个或一个) </p>
<p><a href="eulayesbutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaYesButton&lt;/strong&gt;](eulayesbutton-xml-element.md)"><strong>eulaYesButton</strong></a> (零个或一个) </p>
<p><a href="finishtext-xml-element.md" data-raw-source="[&lt;strong&gt;finishText&lt;/strong&gt;](finishtext-xml-element.md)"><strong>finishText</strong></a> (零个或一个) </p>
<p><a href="finishtitle-xml-element.md" data-raw-source="[&lt;strong&gt;finishTitle&lt;/strong&gt;](finishtitle-xml-element.md)"><strong>finishTitle</strong></a> (零个或一个) </p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong></a> (零个或一个) </p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>图标</strong></a> (零个或一个) </p>
<p><a href="installheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;installHeaderTitle&lt;/strong&gt;](installheadertitle-xml-element.md)"><strong>installHeaderTitle</strong></a> (零个或一个) </p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong></a> (零个或一个) </p>
<p><a href="welcomeintro-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeIntro&lt;/strong&gt;](welcomeintro-xml-element.md)"><strong>welcomeIntro</strong></a> (零个或一个) </p>
<p><a href="welcometitle-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeTitle&lt;/strong&gt;](welcometitle-xml-element.md)"><strong>welcomeTitle</strong></a> (零个或一个) </p></td>
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

您可以使用 **语言** 元素本地化和自定义文本、图标和 DPInst 在其向导页上显示的位图。 图标表示 Microsoft Windows 任务栏和 Windows desktop 上的 DPInst。

DPInst 还将此图标用于添加到控制面板中的 " **程序和功能** " 的项。 这些条目表示 DPInst 安装的 [驱动程序包](/windows-hardware/drivers) 。

**注意**   在早于 Windows Vista 的 Windows 版本中，DPInst 将这些条目添加到控制面板中的 "**添加或删除程序**"。

 

若要自定义仅限英文版本的 DPInst 中显示在向导页上的项，请使用指定英语 (标准) 语言的 **语言** 元素，并包含自定义项的 **语言** 元素的子元素。 若要本地化和自定义在多语言版本的 DPInst 的 DPInst 向导页中显示的项，请使用指定语言的 **语言** 元素，并包含自定义项的 **语言** 元素的子元素。

下面的代码示例演示了一个 **语言** 元素，该元素指定英语 (标准) 语言，并包括自定义 **dpinstTitle** 和 **welcomeTitle** XML 子元素。 指定自定义文本的文本以粗体显示。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <dpinstTitle>Toaster Device Installer</dpinstTitle>
    <welcomeTitle>Welcome to the toaster Installer!</welcomeTitle>
    ...
  </language>
  ...
</dpinst>
```

如果未指定 **dpinstTitle** 元素，则 DPInst 将显示默认的 "欢迎使用" 页上显示的默认标题栏文本。

## <a name="see-also"></a>另请参阅


[**dpinstTitle**](dpinsttitle-xml-element.md)

[**协议**](eula-xml-element.md)

[**eulaHeaderTitle**](eulaheadertitle-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**eulaYesButton**](eulayesbutton-xml-element.md)

[**finishText**](finishtext-xml-element.md)

[**finishTitle**](finishtitle-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**按钮**](icon-xml-element.md)

[**installHeaderTitle**](installheadertitle-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

[**welcomeIntro**](welcomeintro-xml-element.md)

[**welcomeTitle**](welcometitle-xml-element.md)

 

