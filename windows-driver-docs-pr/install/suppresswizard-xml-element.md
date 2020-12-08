---
title: suppressWizard XML 元素
description: SuppressWizard XML 元素是一个空元素，用于将 suppressWizard 标志设置为 ON，后者配置 DPInst 以禁止显示向导页和 DPInst 生成的其他用户消息。
keywords:
- suppressWizard XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- suppressWizard XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3cb9696d410f98b85293dac725373849ed640554
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828605"
---
# <a name="suppresswizard-xml-element"></a>suppressWizard XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**SuppressWizard** XML 元素是一个空元素，用于将 **suppressWizard** 标志设置为 ON，后者配置 DPInst 以禁止显示向导页和 DPInst 生成的其他用户消息。

**元素标记**

```cpp
<suppressWizard>
```

**XML 特性**

无

**元素信息**

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

 

**备注**

默认情况下， **suppressWizard** 标志设置为 OFF。 可以通过将 **suppressWizard** XML 元素包含为 dpinst 描述符文件中 **dpinst** XML 元素的子元素或使用 **/sw** 命令行开关，将 **suppressWizard** 标志设置为 ON。 **SuppressWizard** 标志适用于 **suppressEulaPage** 标志。

下面的代码示例演示了 **suppressWizard** 元素。

```cpp
<dpinst>
  ...
  <suppressWizard/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

