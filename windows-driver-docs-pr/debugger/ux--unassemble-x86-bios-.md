---
title: ux（取消汇编 x86 BIOS）
description: Ux 命令显示基于 x86 的 BIOS 代码的指令集。
keywords:
- ux (Unassemble x86 BIOS) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ux (Unassemble x86 BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ee67e47e46801815660f077defc7ae2101dc359f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802987"
---
# <a name="ux-unassemble-x86-bios"></a>ux（取消汇编 x86 BIOS）


**Ux** 命令显示基于 X86 的 BIOS 代码的指令集。

`ux [Address]`

## <a name="span-idddk_cmd_unassemble_x86_bios_dbgspanspan-idddk_cmd_unassemble_x86_bios_dbgspanparameters"></a><span id="ddk_cmd_unassemble_x86_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_X86_BIOS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定基于 x86 的 BIOS 代码内的内存偏移量。 如果省略此参数或指定零，则默认偏移量为 BIOS 开始。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅基于 x86</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试 BIOS 代码的详细信息，请参阅 [调试 Bios 代码](debugging-bios-code.md)。

<a name="remarks"></a>备注
-------

调试器显示从 *地址* 偏移量开始的前八行代码生成的指令。

若要使 **ux** 命令正常工作，调试器必须提供 HAL 符号。 如果调试器找不到这些符号，调试器将显示 "无法解决" 错误。

 

 





