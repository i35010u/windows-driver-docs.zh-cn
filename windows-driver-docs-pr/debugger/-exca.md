---
title: exca
description: Exca 扩展显示 PC 卡中断控制器 (PCIC) Exchangable 卡体系结构 (ExCA) 寄存器。
ms.assetid: a395f7f3-0e1d-4f4c-80a1-018ca52a20fd
keywords:
- PCIC （PC 卡中断控制器）
- ExCA 寄存器
- exca Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- exca
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 474a70bed6dda22d453db1b7b4c462d4ecaaaf43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577099"
---
# <a name="exca"></a>!exca


**！ Exca**扩展显示 PC 卡中断控制器 (PCIC) Exchangable 卡体系结构 (ExCA) 寄存器。

```dbgcmd
!exca BasePort.SocketNumber
```

## <a name="span-idddkexcadbgspanspan-idddkexcadbgspanparameters"></a><span id="ddk__exca_dbg"></span><span id="DDK__EXCA_DBG"></span>参数


<span id="_______BasePort______"></span><span id="_______baseport______"></span><span id="_______BASEPORT______"></span> *BasePort*   
指定 PCIC 的基本端口。

<span id="_______SocketNumber______"></span><span id="_______socketnumber______"></span><span id="_______SOCKETNUMBER______"></span> *SocketNumber*   
指定 PCIC ExCA 寄存器的套接字数。

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

 

**！ Exca**扩展功能仅适用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

[ **！ Cbreg** ](-cbreg.md)扩展可用于显示 CardBus 套接字寄存器和 CardBus ExCA 注册地址。

 

 





