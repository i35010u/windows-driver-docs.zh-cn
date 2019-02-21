---
title: srb
description: Srb 扩展显示有关 SCSI 请求块 (SRB) 的信息。
ms.assetid: 38f40a78-c991-465e-9203-a8171d1a86f6
keywords:
- srb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- srb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82286326ad1717073b0e778dd4d891596f1e9598
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542785"
---
# <a name="srb"></a>!srb


**！ Srb**扩展显示有关 SCSI 请求块 (SRB) 的信息。

```dbgcmd
!srb Address 
```

## <a name="span-idddksrbdbgspanspan-idddksrbdbgspanparameters"></a><span id="ddk__srb_dbg"></span><span id="DDK__SRB_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定目标计算机上的 SRB 十六进制的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Srb 有关的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

SRB 是用来通信从 SCSI 类驱动程序到 SCSI 端口驱动程序的 I/O 请求的系统定义的结构。

 

 





