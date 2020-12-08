---
title: cbreg
description: Cbreg 扩展显示 CardBus 套接字寄存器和 CardBus Exchangable 卡体系结构 (ExCA) 寄存器。
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
ms.openlocfilehash: 47cc82c79231dcd22e7de88c1a23e74448ddf09a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814091"
---
# <a name="cbreg"></a>!cbreg


**！ Cbreg** Extension 显示 Cardbus 套接字寄存器和 Cardbus Exchangable 卡体系结构 (ExCA) 寄存器。

```dbgsyntax
    !cbreg [%%]Address 
```

## <a name="span-idddk__cbreg_dbgspanspan-idddk__cbreg_dbgspanparameters"></a><span id="ddk__cbreg_dbg"></span><span id="DDK__CBREG_DBG"></span>参数


<span id="_______________"></span> **%%**   
指示 *地址* 是物理地址而不是虚拟地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的寄存器的地址。

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

 

**！ Cbreg** 扩展仅适用于基于 x86 的目标计算机。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

[**！ Exca**](-exca.md)扩展可用于按套接号显示 PCIC exca 寄存器。

 

 





