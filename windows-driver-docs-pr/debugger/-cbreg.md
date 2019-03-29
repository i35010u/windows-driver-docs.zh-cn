---
title: cbreg
description: Cbreg 扩展显示 CardBus 套接字寄存器并 CardBus Exchangable 卡体系结构 (ExCA) 注册。
ms.assetid: 7943e152-b1c9-464c-a0ad-3beac48884d2
keywords:
- CardBus
- ExCA 寄存器
- cbreg Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cbreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0633d985e91f628746d2bf30d1f055654c7320dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576364"
---
# <a name="cbreg"></a>!cbreg


**！ Cbreg**扩展显示 CardBus 套接字寄存器和 CardBus Exchangable 卡体系结构 (ExCA) 注册。

```dbgsyntax
    !cbreg [%%]Address 
```

## <a name="span-idddkcbregdbgspanspan-idddkcbregdbgspanparameters"></a><span id="ddk__cbreg_dbg"></span><span id="DDK__CBREG_DBG"></span>参数


<span id="_______________"></span> **%%**   
指示*地址*是物理地址，而不是虚拟的地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的寄存器的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

**！ Cbreg**扩展功能仅适用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

[ **！ Exca** ](-exca.md)扩展可用于通过套接字数量显示 PCIC ExCA 寄存器。

 

 





