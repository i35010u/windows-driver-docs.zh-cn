---
title: minipkd.req
description: Minipkd.req 扩展指定的适配器或设备上显示有关当前处于活动状态的请求的所有信息。
ms.assetid: 5edc00dd-9a0b-4576-a3ec-11ce22163e95
keywords:
- minipkd.req Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.req
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a1bfc79973c5aa23d3d92e762ce5e8258ea0c3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523233"
---
# <a name="minipkdreq"></a>!minipkd.req


**！ Minipkd.req**扩展指定的适配器或设备上显示所有当前处于活动状态的请求有关的信息。

```dbgcmd
!minipkd.req Adapter 
!minipkd.req Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span> *Adapter*   
指定适配器的地址。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *设备*   
指定逻辑单元扩展 (LUN) 设备的物理设备对象 (PDO)。

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

中找不到 LUN 的 PDO **DevObj**字段[ **！ minipkd.adapters** ](-minipkd-adapters.md)显示。

 

 





