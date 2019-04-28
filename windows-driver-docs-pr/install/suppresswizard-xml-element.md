---
title: suppressWizard XML 元素
description: SuppressWizard XML 元素是空元素，用于 suppressWizard 标志设置为 ON，将配置 DPInst 禁止显示的向导页和 DPInst 生成其他用户消息。
ms.assetid: fb72ff30-7d93-4531-9115-c299fabec7e7
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
ms.openlocfilehash: 72c24e2bbd3ea296555b4563294ae229dd022233
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339635"
---
# <a name="suppresswizard-xml-element"></a>suppressWizard XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**SuppressWizard** XML 元素为空元素，用于设置**suppressWizard**该 DPInst 标志为 ON，将配置 DPInst 禁止显示的向导页和其他用户消息生成。

**元素标记**

```cpp
<suppressWizard>
```

**XML 特性**

无

**元素的信息**

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
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

**注释**

默认情况下**suppressWizard**标志设置为 OFF。 可以设置**suppressWizard**通过包括标志为 ON **suppressWizard**作为子元素的 XML 元素**dpinst** DPInst 描述符文件中或通过使用 XML 元素 **/sw** 命令行开关。 **SuppressWizard**标志适用于**suppressEulaPage**标志。

下面的代码示例演示**suppressWizard**元素。

```cpp
<dpinst>
  ...
  <suppressWizard/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






