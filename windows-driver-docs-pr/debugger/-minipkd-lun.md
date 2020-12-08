---
title: minipkd
description: Minipkd 扩展显示 (LUN) 的指定逻辑单元扩展的详细信息。
keywords:
- minipkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.lun
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa2e660230368003d3c7998af7d1d3608d52df88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799867"
---
# <a name="minipkdlun"></a>!minipkd.lun


**！ Minipkd** 扩展显示 (lun) 的指定逻辑单元扩展的详细信息。

```dbgcmd
!minipkd.lun LUN 
!minipkd.lun Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______LUN______"></span><span id="_______lun______"></span>*LUN*   
指定 LUN 的地址。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span>*设备*   
指定 LUN (PDO) 的物理设备对象。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

LUN 通常称为 *设备*。 因此，此扩展显示有关适配器上设备的信息。

可以通过 (的地址指定 LUN，该地址可以在 [**！ minipkd**](-minipkd-adapters.md)显示) 的 **LUN** 字段中找到，也可以通过其物理设备对象 (，可以在 **！ minipkd**) 显示的 **DevObj** 字段中找到该对象。

 

 





