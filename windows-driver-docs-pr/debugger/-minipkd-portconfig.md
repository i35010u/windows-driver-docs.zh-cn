---
title: minipkd.portconfig
description: Minipkd.portconfig 扩展显示有关指定 PORT_CONFIGURATION_INFORMATION 数据结构的信息。
ms.assetid: efc527c4-0340-4976-9126-d3e32286fc64
keywords:
- minipkd.portconfig Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.portconfig
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1dc61790f8281c6260401b979198b2ed833f7c4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336086"
---
# <a name="minipkdportconfig"></a>!minipkd.portconfig


**！ Minipkd.portconfig**扩展显示有关指定的端口的信息\_配置\_信息数据结构。

```dbgcmd
!minipkd.portconfig PortConfig 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______PortConfig______"></span><span id="_______portconfig______"></span><span id="_______PORTCONFIG______"></span> *PortConfig*   
指定的地址的端口\_配置\_信息数据结构。

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

*PortConfig*中可以找到地址**端口配置信息**字段[ **！ minipkd.adapter** ](-minipkd-adapter.md)显示。

 

 





