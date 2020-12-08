---
title: whattime
description: Whattime 扩展将滴答计数转换为标准时间值。
keywords:
- 时钟周期 (tick count)
- whattime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whattime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d13463ca5e38c67b6ab1334907ce2985ee3c352
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823581"
---
# <a name="whattime"></a>!whattime


**！ Whattime** extension 将滴答计数转换为标准时间值。

```dbgcmd
!whattime Ticks
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Ticks______"></span><span id="_______ticks______"></span><span id="_______TICKS______"></span>*刻度*   
计时周期数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

输出显示为 *HH： MM： SS*。 以下是示例：

```dbgcmd
kd> !whattime 29857ae4
696613604 Ticks in Standard Time:  15:02:16.040s
```

 

 





