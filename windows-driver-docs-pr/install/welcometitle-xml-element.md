---
title: welcomeTitle XML 元素
description: welcomeTitle XML 元素
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
ms.openlocfilehash: 4131a6f9fac9d70140faa7df83f4401ce5d2e87c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819467"
---
# <a name="welcometitle-xml-element"></a>welcomeTitle XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**WelcomeTitle** XML 元素自定义显示在 DPInst 欢迎页顶部的欢迎标题的粗体文本。

### <a name="element-tag"></a>元素标记

```cpp
<welcomeTitle>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>自定义欢迎页面顶部标题文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示了 **welcomeTitle** 元素自定义欢迎页上的标题文本。 指定自定义欢迎标题的文本以粗体显示。

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

如果未指定 **welcomeTitle** 元素，则 DPInst 将显示默认 "欢迎使用" 页上显示的默认 "欢迎使用" 标题。

## <a name="see-also"></a>请参阅


[**语言**](language-xml-element.md)

 

