---
title: pmssa
description: Pmssa 扩展显示指定的处理器最低状态保存区域 (也称为 Min-StateSave 区域) 。
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
ms.openlocfilehash: 296f4457b7b8b086f77f2e1e762c6b5ca5ff636d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824393"
---
# <a name="pmssa"></a>!pmssa


**！ Pmssa** extension 显示指定的处理器最低状态保存区域 (也称为 Min-StateSave 区域) 。

此扩展只能与基于 Itanium 的目标计算机一起使用。

```dbgcmd
!pmssa Address
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定处理器 Min-StateSave 区域的地址。

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

 

 

 





