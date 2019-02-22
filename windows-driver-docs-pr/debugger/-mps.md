---
title: mps
description: 管理包扩展显示目标计算机的 BIOS 信息为 Intel 包含多个处理器规范 (MP)。
ms.assetid: b6ee2eac-ef3c-403a-83ca-fe45506a8c4e
keywords:
- mp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56ebf64bd0fbe009f043be7f9d7f0aeb5386330e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533007"
---
# <a name="mps"></a>!mps


**！ Mp**扩展显示的目标计算机的 BIOS 信息为 Intel 包含多个处理器规范 (MP)。

```dbgcmd
!mps [Address] 
```

## <a name="span-idddkmpsdbgspanspan-idddkmpsdbgspanparameters"></a><span id="ddk__mps_dbg"></span><span id="DDK__MPS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
在 BIOS 中指定的 MP 表十六进制的地址。 如果省略此属性，从 HAL 获取信息。 这将需要 HAL 符号。

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

 

此扩展命令仅用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 BIOS 调试的详细信息，请参阅[调试 BIOS 代码](debugging-bios-code.md)。 有关管理包的详细信息，请参阅 Intel 包含多个处理器规范的适当版本。

 

 





