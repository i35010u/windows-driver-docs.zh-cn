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
ms.openlocfilehash: 3ebc3a1ec42dcc84e3047046db859698fdaed04e
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025180"
---
# <a name="prcb"></a>!prcb


**! Prcb** extension 显示处理器控制块 (prcb)。

```dbgcmd
!prcb [Processor]
```

## <a name="span-idddk__prcb_dbgspanspan-idddk__prcb_dbgspanparameters"></a><span id="ddk__prcb_dbg"></span><span id="DDK__PRCB_DBG"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要从中检索 PRCB 信息的处理器。 如果省略了*processor* , 将使用处理器零。

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
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 PCR 和 PRCB 的信息, 请参阅*Microsoft Windows 内部机制*, 标记为 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

PRCB 是处理器控件区域 (PCR) 的扩展。 若要显示 PCR, 请使用[ **! PCR**](-pcr.md)扩展。

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

 

 





