---
title: bushnd
description: Bushnd 扩展显示 HAL BUS_HANDLER 结构。
keywords:
- bushnd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bushnd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1177be2113ef1111e258625ea15fbf7f3caf81d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814125"
---
# <a name="bushnd"></a>!bushnd


**！ Bushnd** EXTENSION 显示 HAL 总线 \_ 处理程序结构。

```dbgsyntax
    !bushnd [Address] 
```

## <a name="span-idddk__bushnd_dbgspanspan-idddk__bushnd_dbgspanparameters"></a><span id="ddk__bushnd_dbg"></span><span id="DDK__BUSHND_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 HAL 总线 \_ 处理程序结构的十六进制地址。 如果省略， **！ bushnd** 将显示一个总线列表和该处理程序的基址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





