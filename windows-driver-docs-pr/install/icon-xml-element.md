---
title: icon XML 元素
description: icon XML 元素
ms.assetid: 1d5acaf7-ef90-40f7-a2f9-f1002207f3fb
keywords:
- 图标 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- icon XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 21ea8c4f5714d95833c43ed65bea650063c1dc1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364967"
---
# <a name="icon-xml-element"></a>icon XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**图标**XML 元素指定 DPInst DPInst EULA 页面显示一个自定义图标的源文件。 DPInst 使用此图标来表示 DPInst 桌面 Microsoft Windows 任务栏上。 DPInst 还使用此图标表示的项[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，这将增加 DPInst**程序和功能**控制面板中

**请注意**  在 Windows Vista 之前 DPInst 添加到驱动程序包的条目**添加或删除程序**控制面板中。

 

### <a name="element-tag"></a>元素标记

```cpp
<icon>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>或<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>指定包含 DPInst DPInst EULA 页面显示的图标的源文件的字符串。 图标文件必须位于 DPInst 根目录下，这是包含 DPInst 可执行文件的目录 (<em>DPInst.exe</em>)，或在 DPInst 根目录下的子目录中。 如果图标文件的子目录中，指定是相对于 DPInst 根目录的完全限定的文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

**图标**自定义，但未进行本地化，如果它是子元素的元素**dpinst** XML 元素。 **图标**元素是自定义的如果它是子元素的已本地化**语言**XML 元素。

下面的代码示例演示**图标**元素，它指定数据\\Small.ico 作为 DPInst DPInst EULA 页面上显示的自定义图标源。 指定自定义图标文件的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <icon>Data\Eula.ico</icon>
  ...
</dpinst>
```

如果**图标**元素未指定，DPInst 显示默认图标。 不能更改此图标的位置。

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**language**](language-xml-element.md)

 

 






