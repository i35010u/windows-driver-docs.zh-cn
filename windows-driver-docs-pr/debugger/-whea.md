---
title: whea
description: Whea 扩展显示顶级的 Windows 硬件错误体系结构 (WHEA) 信息。
ms.assetid: 5d621507-74e7-4a43-8600-88dca29e461d
keywords:
- whea Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whea
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64be5d0163bb821ad30c1ebe65d26ce7b41c6ecf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342831"
---
# <a name="whea"></a>!whea


**！ Whea**扩展显示顶级的 Windows 硬件错误体系结构 (WHEA) 信息。

```dbgcmd
!whea 
```

## <span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>


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

[ **！ Errrec** ](-errrec.md)并[ **！ errpkt** ](-errpkt.md)扩展可用于显示 WHEA 的其他信息。 WHEA 的常规信息，请参阅[Windows 硬件错误体系结构 (WHEA)](https://go.microsoft.com/fwlink/p/?linkid=153571) Windows Driver Kit (WDK) 文档中。

<a name="remarks"></a>备注
-------

下面的示例演示 （截断） 的输出 **！ whea**扩展：

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
                    : wrapper @ fffffa8007cf4c3e  record @ fffffa8007cf4c6e
                    : wrapper @ fffffa8007cf587c  record @ fffffa8007cf58ac
                    : wrapper @ fffffa8007cf64ba  record @ fffffa8007cf64ea
                    : wrapper @ fffffa8007cf70f8  record @ fffffa8007cf7128
                    : wrapper @ fffffa8007cf7d36  record @ fffffa8007cf7d66
                    : wrapper @ fffffa8007cf8974  record @ fffffa8007cf89a4
                    : wrapper @ fffffa8007cf95b2  record @ fffffa8007cf95e2
                    : wrapper @ fffffa8007cfa1f0  record @ fffffa8007cfa220
                    : wrapper @ fffffa8007cfae2e  record @ fffffa8007cfae5e
                    : wrapper @ fffffa8007cfba6c  record @ fffffa8007cfba9c
                    : wrapper @ fffffa8007cfc6aa  record @ fffffa8007cfc6da
                    : wrapper @ fffffa8007cfd2e8  record @ fffffa8007cfd318
                    : wrapper @ fffffa8007cfdf26  record @ fffffa8007cfdf56
                    : wrapper @ fffffa8007cfeb64  record @ fffffa8007cfeb94
                    : wrapper @ fffffa8007cff7a2  record @ fffffa8007cff7d2
   Descriptor       : @ fffffa8006413328
      Length                     : 3cc
      Max Raw Data Length        : 392
      Num Records To Preallocate : 10
      Max Sections Per Record    : 3
      Error Source ID            : 0
      Flags                      : 00000000
Error Source 1 @ fffffa8007d00bc0
   Notify Type      : Corrected Machine Check
   Type             : 0x1 (CMC)
   Error Count      : 0
   Record Count     : 10
   Record Length    : c3e
   Error Records    : wrapper @ fffffa8007d01000  record @ fffffa8007d01030
                    : wrapper @ fffffa8007d01c3e  record @ fffffa8007d01c6e
                    : wrapper @ fffffa8007d0287c  record @ fffffa8007d028ac
                    : wrapper @ fffffa8007d034ba  record @ fffffa8007d034ea
                    : wrapper @ fffffa8007d040f8  record @ fffffa8007d04128
                    : wrapper @ fffffa8007d04d36  record @ fffffa8007d04d66
                    : wrapper @ fffffa8007d05974  record @ fffffa8007d059a4
                    : wrapper @ fffffa8007d065b2  record @ fffffa8007d065e2
                    : wrapper @ fffffa8007d071f0  record @ fffffa8007d07220
                    : wrapper @ fffffa8007d07e2e  record @ fffffa8007d07e5e
                    : wrapper @ fffffa8007d08a6c  record @ fffffa8007d08a9c
                    : wrapper @ fffffa8007d096aa  record @ fffffa8007d096da
                    : wrapper @ fffffa8007d0a2e8  record @ fffffa8007d0a318
                    : wrapper @ fffffa8007d0af26  record @ fffffa8007d0af56
                    : wrapper @ fffffa8007d0bb64  record @ fffffa8007d0bb94
                    : wrapper @ fffffa8007d0c7a2  record @ fffffa8007d0c7d2
   Descriptor       : @ fffffa8007d00c28
      Length                     : 3cc
      Max Raw Data Length        : 392
      Num Records To Preallocate : 10
      Max Sections Per Record    : 3
      Error Source ID            : 1
      Flags                      : 00000000
Error Source 2 @ fffffa8007d00770
   Notify Type      : Non-Maskable Interrupt
   Type             : 0x3 (NMI)
   Error Count      : 1
   Record Count     : 1
   Record Length    : 1f8
   Error Records    : wrapper @ fffffa800631b2c0  record @ fffffa800631b2f0
   Descriptor       : @ fffffa8007d007d8
      Length                     : 3cc
      Max Raw Data Length        : 100
      Num Records To Preallocate : 1
      Max Sections Per Record    : 1
      Error Source ID            : 2
      Flags                      : 00000000
Error Source 3 @ fffffa8007d0dbc0
   Notify Type      : BOOT Error Record
   Type             : 0x7 (BOOT)
   Error Count      : 0
   Record Count     : 1
   Record Length    : 4f8
   Error Records    : wrapper @ 0000000000000000  record @ 0000000000000030
   Descriptor       : @ fffffa8007d0dc28
      Length                     : 3cc
      Max Raw Data Length        : 400
      Num Records To Preallocate : 1
      Max Sections Per Record    : 1
      Error Source ID            : 3
      Flags                      : 00000000

. . . . 
```

 

 





