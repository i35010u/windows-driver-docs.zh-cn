---
title: whatperftime
description: Whatperftime 扩展将标准时间值转换为高分辨率性能计数器的值。
ms.assetid: ff11a51f-4e25-4cf3-be19-d38361c441e9
keywords:
- 性能计数
- whatperftime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whatperftime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bee6ad77a46605e333075c1f43e7ea53648567b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566436"
---
# <a name="whatperftime"></a>!whatperftime


**！ Whatperftime**扩展将高分辨率性能计数器的值转换为标准时间值。

```dbgcmd
!whatperftime Count
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
性能计数器的时钟值。

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

可以使用 **！ whatperftime**若要通过调用检索的值转换**QueryPerformanceCounter**。 在软件跟踪还找到性能计数器时间值。

输出显示为*HH:MM:SS.mmm*。 下面是一个示例：

```dbgcmd
kd> !whatperftime 304589
3163529 Performance Counter in Standard Time: .004.313s
```

 

 





