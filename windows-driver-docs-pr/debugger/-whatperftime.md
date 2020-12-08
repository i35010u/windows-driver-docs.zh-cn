---
title: whatperftime
description: Whatperftime 扩展将高分辨率性能计数器值转换为标准时间值。
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
ms.openlocfilehash: 48464d91ddd48646a2f18493be4c37bd3413881f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823579"
---
# <a name="whatperftime"></a>!whatperftime


**！ Whatperftime** extension 将高分辨率性能计数器值转换为标准时间值。

```dbgcmd
!whatperftime Count
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
性能计数器时钟值。

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

可以使用 **！ whatperftime** 转换通过调用 **QueryPerformanceCounter** 检索到的值。 性能计数器时间值也可在软件跟踪中找到。

输出显示为 *HH： MM： SS*。 以下是示例：

```dbgcmd
kd> !whatperftime 304589
3163529 Performance Counter in Standard Time: .004.313s
```

 

 





