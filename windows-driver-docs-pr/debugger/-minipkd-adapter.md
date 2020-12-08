---
title: minipkd 适配器
description: Minipkd 扩展显示有关指定适配器的信息。
keywords:
- minipkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ce82c60aa0bd6c1564b8f1cc94734309d184a7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830817"
---
# <a name="minipkdadapter"></a>!minipkd.adapter


**！ Minipkd** 扩展显示有关指定适配器的信息。

```dbgcmd
!minipkd.adapter Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定适配器的地址。

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

可以在 [**！ minipkd**](-minipkd-adapters.md)显示的 " **DevExt** " 字段中找到适配器的地址。

 

 





