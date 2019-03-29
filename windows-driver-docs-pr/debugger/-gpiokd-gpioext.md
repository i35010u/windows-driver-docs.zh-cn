---
title: gpiokd.gpioext
description: Gpiokd.gpioext 命令显示有关 GPIO 控制器的信息。
ms.assetid: D5DB5166-A173-409E-A6A1-3872A22D19E1
keywords:
- gpiokd.gpioext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.gpioext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd5d879945651d9bce11aa971c237211ff393594
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563257"
---
# <a name="gpiokdgpioext"></a>!gpiokd.gpioext


**！ Gpiokd.gpioext**命令显示有关 GPIO 控制器的信息。

```dbgcmd
!gpiokd.gpioext ExtensionAddress [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______ExtensionAddress______"></span><span id="_______extensionaddress______"></span><span id="_______EXTENSIONADDRESS______"></span> *ExtensionAddress*   
地址[\_设备\_扩展](gpio-extensions.md#data-structures-used-by-the-gpio-commands)结构，它表示 GPIO 控制器。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定所显示的信息的标志。 此参数是一个或多个下列标志的按位 OR。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>显示每个单元的固定表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>如果位 0 (0x1) 设置并设置此标志 (0x2)，显示内容包括启用和掩码注册组，每组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>如果位 0 (0x1) 设置并设置此标志 (0x4)，显示内容包括未配置的 pin。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






