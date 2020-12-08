---
title: mps
description: Mps 扩展显示目标计算机 (MP) 的 Intel 多处理器规范的 BIOS 信息。
keywords:
- mps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f1eebd0bc168378dd0d5c10193387e018b619a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831675"
---
# <a name="mps"></a>!mps


**！ Mps** extension 显示目标计算机 (mp) 的 Intel 多处理器规范的 BIOS 信息。

```dbgcmd
!mps [Address] 
```

## <a name="span-idddk__mps_dbgspanspan-idddk__mps_dbgspanparameters"></a><span id="ddk__mps_dbg"></span><span id="DDK__MPS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 BIOS 中 MPS 表的十六进制地址。 如果省略此内容，则从 HAL 获取信息。 这将需要 HAL 符号。

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

 

此扩展命令只能与基于 x86 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 BIOS 调试的详细信息，请参阅 [调试 Bios 代码](debugging-bios-code.md)。 有关 MPS 的详细信息，请参阅英特尔多处理器规范的适当版本。

 

 





