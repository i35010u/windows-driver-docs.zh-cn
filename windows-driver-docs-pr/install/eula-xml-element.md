---
title: eula XML 元素
description: eula XML 元素
keywords:
- eula XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- eula XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f1a5d1ee50ad91ffc650ed1f004c403b2b89be3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813147"
---
# <a name="eula-xml-element"></a>eula XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**Eula** xml 元素是一个空 XML 元素，该元素包含两个属性，这些属性指定一个 eula 文本文件，该文件包含 DPInst eula 页面的自定义文本。

### <a name="element-tag"></a>元素标记

```cpp
<eula>
```

### <a name="xml-attributes"></a>XML 属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>类型</strong></p></td>
<td align="left"><p>供应商提供的 EULA 的类型。 此属性的值必须设置为字符串 "txt"，这表示纯文本文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>路径</strong></p></td>
<td align="left"><p>标识包含 DPInst EULA 页面文本的文件的名称的字符串。 EULA 文本文件必须使用 UTF-8 编码进行编码。 EULA 文件必须位于 DPInst 根目录中，该目录包含 DPInst 可执行文件 (<em>DPInst.exe</em>) ，或 DPInst 根目录下的子目录。 如果 EULA 文件位于子目录中，请指定一个相对于 DPInst 根目录的完全限定文件名。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示一个 **eula** 元素，该元素 *指定 \\Eula409.txt* 包含自定义 eula 文本的数据。 *Eula409.txt* 文件位于 *Data* 目录中，后者必须是 DPInst 根目录下的子目录。 下面显示了使用 EULA 标记指定自定义 EULA 文件的文本 &lt; &gt; 。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eula type="txt" path="Data\Eula409.txt"/>
    ...
  </language>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**语言**](language-xml-element.md)

 

