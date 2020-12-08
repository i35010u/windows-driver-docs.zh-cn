---
title: prcb
description: Prcb 扩展显示处理器控制块 (PRCB) 。
keywords:
- 处理器控制块
- prcb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- prcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b67f10f8bd2f3d81553bec741d2fab8f0c7ec926
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824733"
---
# <a name="prcb"></a>!prcb


**！ Prcb** 扩展显示处理器控制块 (prcb) 。

```dbgcmd
!prcb [Processor]
```

## <a name="span-idddk__prcb_dbgspanspan-idddk__prcb_dbgspanparameters"></a><span id="ddk__prcb_dbg"></span><span id="DDK__PRCB_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要从中检索 PRCB 信息的处理器。 如果省略了 *processor* ，将使用处理器零。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 PCR 和 PRCB 的信息，请参阅 *Microsoft Windows 内部机制*，标记为 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

PRCB 是)  (PCR 的处理器控件区域的扩展。 若要显示 PCR，请使用 [**！ PCR**](-pcr.md) 扩展。

以下是示例：

```dbgcmd
kd> !prcb
PRCB for Processor 0 at e0000000818ba000:
Threads--  Current e0000000818bbe10 Next 0000000000000000 Idle e0000000818bbe10
Number 0 SetMember 00000001
Interrupt Count -- 0000b81f
Times -- Dpc    00000028 Interrupt 000003ff 
         Kernel 00005ef4 User      00000385 
```

 

 





