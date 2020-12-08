---
title: rellist
description: Rellist 扩展显示即插即用关系列表。
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
ms.openlocfilehash: da5d7cca418cfca0e5e64a4a677f5faae0126433
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795217"
---
# <a name="rellist"></a>!rellist


**！ Rellist** 扩展显示即插即用关系列表。

```dbgcmd
!rellist Address [Flags] 
```

## <a name="span-idddk__rellist_dbgspanspan-idddk__rellist_dbgspanparameters"></a><span id="ddk__rellist_dbg"></span><span id="DDK__RELLIST_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定关系列表的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要包含在显示中的其他信息。 这可以是以下位的任意组合 (默认值为零) ：

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示包含 CM \_ 资源 \_ 列表。 显示还包括启动资源列表（如果可用）。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
导致显示 (IO 资源列表) 包含资源需求列表 \_ \_ 。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
使显示包含已翻译的 CM \_ 资源 \_ 列表。

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

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关这些列表结构的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

 

 





