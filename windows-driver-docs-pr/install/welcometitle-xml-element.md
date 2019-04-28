---
title: welcomeTitle XML 元素
description: welcomeTitle XML 元素
ms.assetid: 480b6d02-b8b1-4e3f-9a00-869cc2b93279
keywords:
- welcomeTitle XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- welcomeTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b67cb60d4271241bce77bc60ced1caa50315d56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339283"
---
# <a name="welcometitle-xml-element"></a>welcomeTitle XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**WelcomeTitle** XML 元素自定义欢迎使用 DPInst 欢迎页顶部显示的标题的粗体文本。

### <a name="element-tag"></a>元素标记

```cpp
<welcomeTitle>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>language</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>自定义欢迎页顶部的标题文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**welcomeTitle**元素自定义欢迎页上的标题文本。 指定自定义欢迎使用标题文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <welcomeTitle>Welcome to the toaster Installer!</welcomeTitle>
    ...
  </language>
  ...
</dpinst>
```

如果**welcomeTitle**元素未指定，DPInst 显示默认的欢迎页显示的默认欢迎使用标题。

## <a name="see-also"></a>请参阅


[**language**](language-xml-element.md)

 

 






