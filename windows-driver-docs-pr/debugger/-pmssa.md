---
title: pmssa
description: Pmssa 扩展显示指定的处理器最小状态保存区域 （也称为最小值 StateSave 区域）。
ms.assetid: 55d605bd-0621-4366-8b37-62d462ee1f34
keywords:
- 处理器 minstate 保存区域
- pmssa Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pmssa
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd8c009c07d34b416a2f1542b236ca3fc40853ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335835"
---
# <a name="pmssa"></a>!pmssa


**！ Pmssa**扩展显示指定的处理器最小状态保存区域 （也称为最小值 StateSave 区域）。

此扩展仅用于基于 Itanium 的目标计算机。

```dbgcmd
!pmssa Address
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的处理器最小值 StateSave 区域的地址。

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

 

 

 





