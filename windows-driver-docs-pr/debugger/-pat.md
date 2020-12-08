---
title: 吧
description: Pat 扩展显示目标处理器 (PAT) 寄存器的页属性表。
keywords:
- PAT
- pat Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pat
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f4597947b72ab19dd5c1c098b5ae21f6c2f4fac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828271"
---
# <a name="pat"></a>!pat


**！ Pat** extension 显示了页属性表 (pat) 注册目标处理器。

```dbgcmd
!pat Flag 
!pat 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
如果设置了 *标志* ，则调试器将验证在显示 pat 之前是否存在 pat 功能。

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

 

此扩展命令只能与基于 x86 的目标计算机一起使用。

 

 





