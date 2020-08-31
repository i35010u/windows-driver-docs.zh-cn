---
title: scanHardware XML 元素
description: scanHardware XML 元素
ms.assetid: c1af7238-97e9-4c5f-95ea-fbc9f3cc8279
keywords:
- scanHardware XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- scanHardware XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8ccd201b232c32921aba4af3bfc953e7eefc6795
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096617"
---
# <a name="scanhardware-xml-element"></a>scanHardware XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**ScanHardware** XML 元素是一个空元素，用于将**scanHardware**标志设置为 ON。 将此标志设置为 "开" 可将 DPInst 配置为仅当驱动程序包与计算机中配置的设备匹配并且驱动程序包比设备上当前安装的驱动程序包更匹配时，才为即插即用 (PnP) 函数驱动程序安装 [驱动程序包](./driver-packages.md) 。

### <a name="element-tag"></a>元素标记

```cpp
<scanHardware>
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

默认情况下， **scanHardware** 标志设置为 OFF。 可以通过将**scanHardware** XML 元素包含为 dpinst 描述符文件中**dpinst** XML 元素的子元素或使用 **/sh**命令行开关，将**scanHardware**标志设置为 ON   。

下面的代码示例演示了 **scanHardware** 元素。

```cpp
<dpinst>
  ...
  <scanHardware/>
  ...
</dpinst>
```

 

