---
title: pcrs
description: Pcrs 扩展显示特定于 Intel Itanium 的处理器控制寄存器。
ms.assetid: 45a84a95-86df-4176-ba30-ac93b509f7f7
keywords:
- 处理器控制寄存器 (PCR)
- PCR （处理器控制寄存器）
- pcrs Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcrs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b42efee88384b3e7acabddcb345f0d5d3fd727
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335818"
---
# <a name="pcrs"></a>!pcrs


**！ Pcrs**扩展显示特定于 Intel Itanium 的处理器控制寄存器。

```dbgcmd
!pcrs Address
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定处理器控制的地址注册文件。

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

 

此扩展命令仅用于基于 Itanium 的目标计算机。

<a name="remarks"></a>备注
-------

不要混淆 **！ pcrs**扩展名[ **！ pcr** ](-pcr.md)扩展，它显示处理器控件区域的当前状态。

 

 





