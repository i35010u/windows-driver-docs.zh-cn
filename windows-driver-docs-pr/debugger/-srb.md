---
title: srb
description: Srb 扩展显示有关 SCSI 请求块 (SRB) 的信息。
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
ms.openlocfilehash: 79222024ef11cfeb7c7fc7098dbfb24ec70db1e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799837"
---
# <a name="srb"></a>!srb


**！ Srb** 扩展显示有关 SCSI 请求块 (srb) 的信息。

```dbgcmd
!srb Address 
```

## <a name="span-idddk__srb_dbgspanspan-idddk__srb_dbgspanparameters"></a><span id="ddk__srb_dbg"></span><span id="DDK__SRB_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定目标计算机上 SRB 的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 SRBs 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

SRB 是一个系统定义的结构，用于将 SCSI 类驱动程序发出的 i/o 请求传递给 SCSI 端口驱动程序。

 

 





