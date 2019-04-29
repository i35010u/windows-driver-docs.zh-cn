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
ms.openlocfilehash: 9b2c28fc664e93ae4f4218153477459d5daffd56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356947"
---
# <a name="language-xml-element"></a>language XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**语言**本地化的 XML 元素和自定义 DPInst 其向导页面显示的项。

### <a name="element-tag"></a>元素标记

```cpp
<language>
```

### <a name="xml-attributes"></a>XML 特性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Code</strong></p></td>
<td align="left"><p>十六进制或十进制格式中的语言标识符。</p></td>
</tr>
</tbody>
</table>

 

### <a name="element-information"></a>**元素的信息**

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
<td align="left"><p><a href="dpinsttitle-xml-element.md" data-raw-source="[&lt;strong&gt;dpinstTitle&lt;/strong&gt;](dpinsttitle-xml-element.md)"><strong>dpinstTitle</strong> </a> （零个或一个）</p>
<p><a href="eula-xml-element.md" data-raw-source="[&lt;strong&gt;eula&lt;/strong&gt;](eula-xml-element.md)"><strong>最终用户许可协议</strong></a> （零个或一个）</p>
<p><a href="eulaheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;eulaHeaderTitle&lt;/strong&gt;](eulaheadertitle-xml-element.md)"><strong>eulaHeaderTitle</strong> </a> （零个或一个）</p>
<p><a href="eulanobutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaNoButton&lt;/strong&gt;](eulanobutton-xml-element.md)"><strong>eulaNoButton</strong> </a> （零个或一个）</p>
<p><a href="eulayesbutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaYesButton&lt;/strong&gt;](eulayesbutton-xml-element.md)"><strong>eulaYesButton</strong> </a> （零个或一个）</p>
<p><a href="finishtext-xml-element.md" data-raw-source="[&lt;strong&gt;finishText&lt;/strong&gt;](finishtext-xml-element.md)"><strong>finishText</strong> </a> （零个或一个）</p>
<p><a href="finishtitle-xml-element.md" data-raw-source="[&lt;strong&gt;finishTitle&lt;/strong&gt;](finishtitle-xml-element.md)"><strong>finishTitle</strong> </a> （零个或一个）</p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong> </a> （零个或一个）</p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>图标</strong></a> （零个或一个）</p>
<p><a href="installheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;installHeaderTitle&lt;/strong&gt;](installheadertitle-xml-element.md)"><strong>installHeaderTitle</strong> </a> （零个或一个）</p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong> </a> （零个或一个）</p>
<p><a href="welcomeintro-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeIntro&lt;/strong&gt;](welcomeintro-xml-element.md)"><strong>welcomeIntro</strong> </a> （零个或一个）</p>
<p><a href="welcometitle-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeTitle&lt;/strong&gt;](welcometitle-xml-element.md)"><strong>welcomeTitle</strong> </a> （零个或一个）</p></td>
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

可以使用**语言**元素本地化和自定义文本、 图标和 DPInst 其向导页面显示的位图。 图标表示 DPInst 上的 Microsoft Windows 任务栏和 Windows 桌面。

DPInst 还使用此图标添加到的项**程序和功能**控制面板中。 这些条目都代表[驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)DPInst 安装。

**请注意**  在版本的 Windows 早于 Windows Vista，DPInst 添加到这些条目**添加或删除程序**控制面板中。

 

若要自定义 DPInst 纯英文版中的向导页面显示的项，请使用**语言**指定的英语 (Standard) 的语言和包括的子元素的元素**语言**自定义项的元素。 若要本地化和自定义 DPInst 的多语言版本中的 DPInst 向导页面显示的项，请使用**语言**指定的语言和包括的子元素的元素**语言**自定义项的元素。

下面的代码示例演示**语言**元素指定的英语 （标准） 语言，包括自定义**dpinstTitle**和**welcomeTitle**XML 子元素。 指定的自定义文本的文本是粗体的字体类型中所示。

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

如果**dpinstTitle**元素未指定，DPInst 显示默认的欢迎页上显示的默认标题栏文本。

## <a name="see-also"></a>请参阅


[**dpinstTitle**](dpinsttitle-xml-element.md)

[**eula**](eula-xml-element.md)

[**eulaHeaderTitle**](eulaheadertitle-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**eulaYesButton**](eulayesbutton-xml-element.md)

[**finishText**](finishtext-xml-element.md)

[**finishTitle**](finishtitle-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**icon**](icon-xml-element.md)

[**installHeaderTitle**](installheadertitle-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

[**welcomeIntro**](welcomeintro-xml-element.md)

[**welcomeTitle**](welcometitle-xml-element.md)

 

 






