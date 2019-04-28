---
title: errpkt
description: Errpkt 扩展显示的 Windows 硬件错误体系结构 (WHEA) 硬件错误数据包的内容。
ms.assetid: cf4b1dfa-3b15-45d4-b5e2-1da7cdbca350
keywords:
- errpkt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errpkt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 130f8a2403ce93bc75b19053234372c627ed0b86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336786"
---
# <a name="errpkt"></a>!errpkt


**！ Errpkt**扩展将显示 Windows 硬件错误体系结构 (WHEA) 硬件错误数据包的内容。

```dbgcmd
!errpkt Address 
```

## <a name="span-idddkubpdbgspanspan-idddkubpdbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定硬件错误数据包的地址。

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
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

仅在 Windows Vista 和更高版本的 Windows 中，可以使用此扩展。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

[ **！ Whea** ](-whea.md)并[ **！ errrec** ](-errrec.md)扩展可用于显示 WHEA 的其他信息。 WHEA 的常规信息，请参阅[Windows 硬件错误体系结构 (WHEA)](https://go.microsoft.com/fwlink/p/?linkid=153571) Windows Driver Kit (WDK) 文档中。

<a name="remarks"></a>备注
-------

下面的示例演示的输出 **！ errpkt**扩展：

```dbgcmd
3: kd> !errpkt fffffa8007cf44da 
   WHEA Error Packet Info Section (@ fffffa8007cf44da)
   Flags            : 0x00000000
   Size             : 0x218
   RawDataLength    : 0x392
   Context          : 0x0000000000000000
   ErrorType        : 0x0 - Processor
   ErrorSeverity    : 0x1 - Fatal
   ErrorSourceId    : 0x0
   ErrorSourceType  : 0x0 - MCE
   Version          : 00000002
   Cpu              : 0000000000000002
   RawDataFormat    : 0x2 - Intel64 MCA

   Raw Data         : Located @ FFFFFA8007CF45F2

Processor Error: (Internal processor error)
This error means either the processor is damaged or perhaps
voltage and/or temperature thresholds have been exceeded.
If the problem continues to occur, replace the processor.
Processor Number : 2
Bank Number      : 0
   Status  :                0
   Address : 0000000000000000 (I)
   Misc    : 0000000000000000 (I)
```

 

 





