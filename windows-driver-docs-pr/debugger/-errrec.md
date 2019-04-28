---
title: errrec
description: Errrec 扩展显示 Windows 硬件错误体系结构 (WHEA) 错误记录的内容。
ms.assetid: 372e4700-0cd7-468d-98e8-b0ead4ebc92f
keywords:
- errrec Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errrec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31285e2986b7f51e798a17cf8bbddfa9f0b07f9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334512"
---
# <a name="errrec"></a>!errrec


**！ Errrec**扩展将显示 Windows 硬件错误体系结构 (WHEA) 错误记录的内容。

```dbgcmd
!errrec Address 
```

## <a name="span-idddkubpdbgspanspan-idddkubpdbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的错误记录的地址。

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

[ **！ Whea** ](-whea.md)并[ **！ errpkt** ](-errpkt.md)扩展可用于显示 WHEA 的其他信息。 WHEA 的常规信息，请参阅[Windows 硬件错误体系结构 (WHEA)](https://go.microsoft.com/fwlink/p/?linkid=153571) Windows Driver Kit (WDK) 文档中。

<a name="remarks"></a>备注
-------

下面的示例演示如何[ **！ whea** ](-whea.md)扩展可用于获取错误记录的地址，然后可以显示此记录的内容 **！ errrec**扩展：

```dbgcmd
3: kd> !whea 
Error Source Table @ fffff800019ca250
13 Error Sources
Error Source 0 @ fffffa80064132c0
   Notify Type      : Machine Check Exception
   Type             : 0x0 (MCE)
   Error Count      : 8
   Record Count     : 10
   Record Length    : c3e
   Error Records    : wrapper @ fffffa8007cf4000  record @ fffffa8007cf4030

. . . . 

# 3: kd> !errrec fffffa8007cf4030 
===============================================================================
## Common Platform Error Record @ fffffa8007cf4030
-------------------------------------------------------------------------------
Revision      : 2.1
Record Id     : 01c9c7ff04e0ff7d
Severity      : Fatal (1)
Length        : 1730
Creator       : Microsoft
Notify Type   : Machine Check Exception
Timestamp     : 4/28/2009 12:54:47
Flags         : 0x00000000
# 
===============================================================================
## Section 0     : Processor Generic
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf40b0
Section       @ fffffa8007cf4188
Offset        : 344
Length        : 192
Flags         : 0x00000001 Primary
Severity      : Fatal

No valid data fields are present.
# 
===============================================================================
## Section 1     : {390f56d5-ca86-4649-95c4-73a408ae5834}
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf40f8
Section       @ fffffa8007cf4248
Offset        : 536
Length        : 658
Flags         : 0x00000000
Severity      : Fatal

*** Unknown section format ***
# 
===============================================================================
## Section 2     : Error Packet
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf4140
Section       @ fffffa8007cf44da
Offset        : 1194
Length        : 536
Flags         : 0x00000000
Severity      : Fatal

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

 

 





