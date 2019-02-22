---
title: minipkd.adapter
description: Minipkd.adapter 扩展显示有关指定的适配器的信息。
ms.assetid: 86cde6f0-9690-41b6-8e81-b9d25d7d6de5
keywords:
- minipkd.adapter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c91403ee1ee2a3a8c8989597be64118fa23ced36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521609"
---
# <a name="minipkdadapter"></a>!minipkd.adapter


**！ Minipkd.adapter**扩展显示有关指定的适配器的信息。

```dbgcmd
!minipkd.adapter Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定适配器的地址。

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

适配器的地址可在**DevExt**字段[ **！ minipkd.adapters** ](-minipkd-adapters.md)显示。

 

 





