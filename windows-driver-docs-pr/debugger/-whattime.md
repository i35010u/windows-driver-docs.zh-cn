---
title: whattime
description: Whattime 扩展将标准时间值转换为的计时周期计数。
ms.assetid: c63e8bad-3a87-4209-b9f0-b6c433c294b2
keywords:
- 时钟周期数
- whattime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whattime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca6f8eb2d6e84afefbc253cdf59d474b0feaf2c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522046"
---
# <a name="whattime"></a>！ whattime


**！ Whattime**扩展将标准时间值转换为的计时周期计数。

```dbgcmd
!whattime Ticks
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Ticks______"></span><span id="_______ticks______"></span><span id="_______TICKS______"></span> *计时周期数*   
计时周期数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

输出显示为*HH:MM:SS.mmm*。 下面是一个示例：

```dbgcmd
kd> !whattime 29857ae4
696613604 Ticks in Standard Time:  15:02:16.040s
```

 

 





