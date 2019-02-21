---
title: rellist
description: Rellist 扩展显示插关系列表。
ms.assetid: ecbf7e35-91c0-4ff4-82a4-53a935920915
keywords:
- rellist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rellist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d632bc61ff186381cbc5e61f2c527014cc43c845
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521443"
---
# <a name="rellist"></a>！ rellist


**！ Rellist**扩展显示插关系列表。

```dbgcmd
!rellist Address [Flags] 
```

## <a name="span-idddkrellistdbgspanspan-idddkrellistdbgspanparameters"></a><span id="ddk__rellist_dbg"></span><span id="DDK__RELLIST_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定关系列表的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要包含在显示中的其他信息。 这可以是以下位 （默认值为零） 的任意组合：

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括 CM\_资源\_列表。 显示内容还包括启动资源列表中，如果可用。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示以包括资源要求列表 (IO\_资源\_列表)。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
将导致显示以包括已翻译的 CM\_资源\_列表。

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

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 这些列表结构有关的信息，请参阅 Windows Driver Kit (WDK) 文档。

 

 





