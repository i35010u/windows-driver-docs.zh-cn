---
title: icon XML 元素
description: icon XML 元素
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
ms.openlocfilehash: b8262c847ed74f1446b91fa359ca4fe19f953c18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828625"
---
# <a name="icon-xml-element"></a>icon XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Icon** XML 元素指定 DPInst 在 DPInst EULA 页上显示的自定义图标的源文件。 DPInst 使用此图标在 Microsoft Windows 任务栏和桌面上表示 DPInst。 DPInst 还为代表 [驱动程序包](./driver-packages.md)的条目使用此图标，DPInst 将其添加到控制面板中的 " **程序和功能** "

**注意**  在 Windows Vista 之前，DPInst 将驱动程序包条目添加到控制面板中的 " **添加或删除程序** "。

 

### <a name="element-tag"></a>元素标记

```cpp
<icon>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a>或<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"> <strong>language</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>指定源文件的字符串，该文件包含 DPInst 在 DPInst EULA 页面上显示的图标。 图标文件必须位于 DPInst 根目录中，该目录包含 DPInst 可执行文件 (<em>DPInst.exe</em>) ，或位于 DPInst 根目录下的子目录中。 如果图标文件位于子目录中，请指定一个相对于 DPInst 根目录的完全限定文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

如果 **icon** 元素是 **dpinst** XML 元素的子元素，则它是自定义的，但未进行本地化。 如果 **icon** 元素为 **language** XML 元素的子元素，则该元素将被自定义和本地化。

下面的代码示例演示了一个 **icon** 元素，该元素将数据 \\ 小 .Ico 指定为 DPINST 在 DPInst EULA 页面上显示的自定义图标的源。 指定自定义图标文件的文本以粗体显示。

```cpp
<dpinst>
  ...
  <icon>Data\Eula.ico</icon>
  ...
</dpinst>
```

如果未指定 **icon** 元素，DPInst 将显示默认图标。 不能更改此图标的位置。

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**语言**](language-xml-element.md)

 

