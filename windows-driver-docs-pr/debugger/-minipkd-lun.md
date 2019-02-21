---
title: minipkd.lun
description: Minipkd.lun 扩展显示有关指定的逻辑单元扩展 (LUN) 的详细的信息。
ms.assetid: f78b2c15-ecfc-4138-b595-a6e3f0f7f93c
keywords:
- minipkd.lun Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.lun
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40bb448e3f0b7486be5406e984f2bd28355cdf21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555880"
---
# <a name="minipkdlun"></a>!minipkd.lun


**！ Minipkd.lun**扩展显示有关指定的逻辑单元扩展 (LUN) 的详细的信息。

```dbgcmd
!minipkd.lun LUN 
!minipkd.lun Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______LUN______"></span><span id="_______lun______"></span> *LUN*   
指定的 LUN 的地址。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *设备*   
Lun 指定物理设备对象 (PDO)。

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

LUN 通常称为*设备*。 因此，此扩展显示有关设备的信息的适配器上。

LUN 可以是指定的地址 (这可在**LUN**字段[ **！ minipkd.adapters** ](-minipkd-adapters.md)显示)，或通过其物理设备对象 （可以是在中找到**DevObj**字段 **！ minipkd.adapters**显示)。

 

 





