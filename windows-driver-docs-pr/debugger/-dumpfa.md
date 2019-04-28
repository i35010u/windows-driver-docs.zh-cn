---
title: dumpfa
description: Dumpfa 扩展显示失败分析项的内容。
ms.assetid: 4516252d-b6c9-4bf4-b435-6c0b3cb0fbc3
keywords:
- 失败分析条目，显示
- 故障分析项
- dumpfa Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dumpfa
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d911ea3688c737d3ddcf6698eaeb3460e725954b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334558"
---
# <a name="dumpfa"></a>!dumpfa


**！ Dumpfa**扩展显示的失败分析项内容。

```dbgcmd
!dumpfa Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定显示的失败分析条目的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Dumpfa**扩展插件可仅用于调试[ **！ 分析**](-analyze.md)扩展，如以下示例所示。

```dbgcmd
0:000> !dumpfa 0x00a34140
DataUsed 3b0
Type =        DEBUG_FLR_MARKER_BUCKET 00010016 - Size = 9
Type =          DEBUG_FLR_MARKER_FILE 0001000d - Size = 16
Type =      DEBUG_FLR_SYSXML_LOCALEID 00004200 - Size = 4
Type =      DEBUG_FLR_SYSXML_CHECKSUM 00004201 - Size = 4
Type =         DEBUG_FLR_READ_ADDRESS 0000000e - Size = 8
Type =          DEBUG_FLR_FAULTING_IP 80000000 - Size = 8
Type =     DEBUG_FLR_MM_INTERNAL_CODE 00001004 - Size = 8
Type = DEBUG_FLR_CPU_MICROCODE_VERSION 0000301f - Size = 28
Type = DEBUG_FLR_CUSTOMER_CRASH_COUNT 0000300b - Size = 8
Type =    DEBUG_FLR_DEFAULT_BUCKET_ID 00010008 - Size = 12
Type =         DEBUG_FLR_BUGCHECK_STR 00000600 - Size = 5
Type = DEBUG_FLR_LAST_CONTROL_TRANSFER 0000000a - Size = 18
Type =           DEBUG_FLR_TRAP_FRAME c0000002 - Size = 8
Type =           DEBUG_FLR_STACK_TEXT 00010005 - Size = 1fb
Type =        DEBUG_FLR_STACK_COMMAND 00010004 - Size = 17
Type =        DEBUG_FLR_OS_BUILD_NAME 0000301e - Size = 9
Type =          DEBUG_FLR_MODULE_NAME 00010006 - Size = 8
Type =           DEBUG_FLR_IMAGE_NAME 00010001 - Size = c
Type =      DEBUG_FLR_IMAGE_TIMESTAMP 80000002 - Size = 8
```

此外可以使用[ **！ asd** ](-asd.md)扩展来调试[ **！ 分析**](-analyze.md)扩展。

 

 





