---
title: npx
description: Npx 扩展显示区域保存浮点寄存器的内容。
ms.assetid: 1601e4fe-0aba-4507-90a1-402c02fba59d
keywords:
- 浮点寄存器保存区域注册
- npx Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- npx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c38fbaa7df1962826a401283c1f79e1c05e35483
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335878"
---
# <a name="npx"></a>!npx


**！ Npx**扩展显示区域保存浮点寄存器的内容。

```dbgcmd
!npx Address
```

## <a name="span-idddknpxdbgspanspan-idddknpxdbgspanparameters"></a><span id="ddk__npx_dbg"></span><span id="DDK__NPX_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的十六进制地址的浮动\_保存\_区域结构。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

此扩展命令仅用于基于 x86 的目标计算机。

 

 





