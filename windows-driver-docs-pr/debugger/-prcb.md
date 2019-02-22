---
title: prcb
description: Prcb 扩展显示处理器控制块 (PRCB)。
ms.assetid: 747695a1-8a5d-4d30-9315-91f4bf7f568e
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
ms.openlocfilehash: d28eb002f743c2382c3a899a65eda6abbaebe550
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525296"
---
# <a name="prcb"></a>!prcb


**！ Prcb**扩展显示处理器控制块 (PRCB)。

```dbgcmd
!prcb [Processor]
```

## <a name="span-idddkprcbdbgspanspan-idddkprcbdbgspanparameters"></a><span id="ddk__prcb_dbg"></span><span id="DDK__PRCB_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定要检索的 PRCB 信息的处理器。 如果*处理器*是省略，就将使用处理器零。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

PCR 和 PRCB 有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

PRCB 是处理器控件区域 (PCR) 的扩展。 若要显示 PCR，请使用[ **！ pcr** ](-pcr.md)扩展。

下面是一个示例：

```dbgcmd
kd> !prcb
PRCB for Processor 0 at e0000000818ba000:
Threads--  Current e0000000818bbe10 Next 0000000000000000 Idle e0000000818bbe10
Number 0 SetMember 00000001
Interrupt Count -- 0000b81f
Times -- Dpc    00000028 Interrupt 000003ff 
         Kernel 00005ef4 User      00000385 
```

 

 





