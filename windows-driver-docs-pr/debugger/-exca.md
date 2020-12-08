---
title: exca
description: Exca 扩展显示 PC-Card 中断控制器 (PCIC) Exchangable 卡体系结构 (ExCA) 寄存器。
keywords:
- 'PCIC (PC 卡中断控制器) '
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
ms.openlocfilehash: d5f9876f4291eeac6435d1cbc9363c4e82b0dc52
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820419"
---
# <a name="exca"></a>!exca


**！ Exca** 扩展显示 PC-Card 中断控制器 (PCIC) Exchangable 卡体系结构 (exca) 寄存器。

```dbgcmd
!exca BasePort.SocketNumber
```

## <a name="span-idddk__exca_dbgspanspan-idddk__exca_dbgspanparameters"></a><span id="ddk__exca_dbg"></span><span id="DDK__EXCA_DBG"></span>参数


<span id="_______BasePort______"></span><span id="_______baseport______"></span><span id="_______BASEPORT______"></span>*BasePort*   
指定 PCIC 的基端口。

<span id="_______SocketNumber______"></span><span id="_______socketnumber______"></span><span id="_______SOCKETNUMBER______"></span>*SocketNumber*   
指定 PCIC 上的 ExCA 寄存器的插槽号。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

**！ Exca** 扩展仅适用于基于 x86 的目标计算机。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

[**！ Cbreg**](-cbreg.md)扩展可用于显示 Cardbus 套接字寄存器和 cardbus ExCA 按地址进行注册。

 

 





