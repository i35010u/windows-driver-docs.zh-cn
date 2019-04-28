---
title: tzinfo
description: Tzinfo 扩展显示的指定散热区域信息结构的内容。
ms.assetid: a30826d8-b7c5-4fbc-a3c3-b7a994eaf7fe
keywords:
- 热感区域信息
- tzinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tzinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645e44da4cd98121b0be693c27f3437b1c10e877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334164"
---
# <a name="tzinfo"></a>!tzinfo


**！ Tzinfo**扩展显示指定散热区域信息结构的内容。

```dbgcmd
!tzinfo Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
你想要显示的散热区域信息结构的地址。

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

若要查看系统的电源功能，请使用[ **！ pocaps** ](-pocaps.md)扩展命令。 若要查看系统的电源策略，请使用[ **！ popolicy** ](-popolicy.md)扩展命令。 有关电源功能和电源策略的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 





