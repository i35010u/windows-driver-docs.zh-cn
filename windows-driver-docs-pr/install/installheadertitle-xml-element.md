---
title: installHeaderTitle XML 元素
description: installHeaderTitle XML 元素
ms.assetid: 43f8611c-9504-46ab-a8f2-06141bf74f1f
keywords:
- installHeaderTitle XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- installHeaderTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a87d1114a158441732120c5bbab12426588f480
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533698"
---
# <a name="installheadertitle-xml-element"></a>installHeaderTitle XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**InstallHeaderTitle** XML 元素自定义安装标头标题 DPInst 安装页上显示的粗体文本。

### <a name="element-tag"></a>元素标记

```cpp
<installHeaderTitle>
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
<td align="left"><p>自定义安装页的标题文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**installHeaderTitle**自定义安装页的标题文本的元素。 指定自定义安装标头标题的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <installHeaderTitle>Installing the software for your Toaster device...</installHeaderTitle>
    ...
  </language>
  ...
</dpinst>
```

如果**installHeaderTitle**元素未指定，DPInst 显示在默认安装页面上显示的默认标题文本。

## <a name="see-also"></a>另请参阅


[**language**](language-xml-element.md)

 

 






