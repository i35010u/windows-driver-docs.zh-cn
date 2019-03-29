---
title: ux（取消汇编 x86 BIOS）
description: Ux 命令显示基于 x86 的 BIOS 代码的指令集。
ms.assetid: d3616255-1a07-4a5d-8171-c8316179a7dc
keywords:
- 用户体验 (反汇编 x86 BIOS) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ux (Unassemble x86 BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b75f50578d869c83b2a5b22357d4a1ed41c477b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576090"
---
# <a name="ux-unassemble-x86-bios"></a>ux（取消汇编 x86 BIOS）


**Ux**命令显示基于 x86 的 BIOS 代码的指令集。

`ux [Address]`

## <a name="span-idddkcmdunassemblex86biosdbgspanspan-idddkcmdunassemblex86biosdbgspanparameters"></a><span id="ddk_cmd_unassemble_x86_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_X86_BIOS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的基于 x86 的 BIOS 代码中的内存偏移量。 如果省略此参数或指定为零，则默认偏移量是个开始的 bios。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 的仅</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何调试 BIOS 代码的详细信息，请参阅[调试 BIOS 代码](debugging-bios-code.md)。

<a name="remarks"></a>备注
-------

调试器将显示从前八行代码，生成的说明开始*地址*偏移量。

若要使**ux**命令工作正常，HAL 符号必须可供调试器。 如果调试器无法找到这些符号，调试器会显示"无法解析"错误。

 

 





