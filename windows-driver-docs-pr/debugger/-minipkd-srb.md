---
title: minipkd.srb
description: Minipkd.srb 扩展显示指定的 SCSI 请求块 (SRB) 数据结构。
ms.assetid: d742a900-f8a8-43a8-b00a-12bb82ca1460
keywords:
- minipkd.srb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.srb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6bcfcb541230dec79bc5653d93a71e3968b7ec0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336034"
---
# <a name="minipkdsrb"></a>!minipkd.srb


**！ Minipkd.srb**扩展显示指定的 SCSI 请求块 (SRB) 数据结构。

```dbgcmd
!minipkd.srb SRB 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______SRB______"></span><span id="_______srb______"></span> *SRB*   
指定 SRB 的地址。

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

当前处于活动状态的所有请求的地址可在*SRB*的输出字段[ **！ minipkd.req** ](-minipkd-req.md)命令。

此扩展显示 SRB，它将发送给颁发 SRB 和其地址和十六进制标志值的 SCSI 的驱动程序的状态。 如果 0x10000 设置中的标志值，此请求当前处于微型端口。

 

 





