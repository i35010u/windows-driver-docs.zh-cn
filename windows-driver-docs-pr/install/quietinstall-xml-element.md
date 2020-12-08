---
title: quietInstall XML 元素
description: quietInstall XML 元素
keywords:
- quietInstall XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- quietInstall XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1ad097823ffcf585bf8ff50cb8f1bde2accc4282
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796019"
---
# <a name="quietinstall-xml-element"></a>quietInstall XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**QuietInstall** XML 元素是一个空元素，该元素将 **quietInstall** 标志设置为 ON，这会将 DPInst 配置为禁止显示向导页和大多数其他用户消息。

### <a name="element-tag"></a>**元素标记**

```cpp
<quietInstall>
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

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

默认情况下， **quietInstall** 标志设置为 OFF。 可以通过在 DPInst 描述符文件中包含 **quietInstall** 元素或使用 **/q** 命令行开关，将 **quietInstall** 标志设置为 ON。 **QuietInstall** 标志用于处理 EULA 页和 **suppressEulaPage** 标志。

下面的代码示例演示了 **quietInstall** 元素

```cpp
<dpinst>
  ...
  <quietInstall/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

