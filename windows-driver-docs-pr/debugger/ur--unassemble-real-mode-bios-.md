---
title: 你 (反汇编实模式下 BIOS)
description: 你的命令显示指定的 16 位实模式代码程序集转换。
ms.assetid: 7ea3421a-3841-47ea-ab40-99d10516bb14
keywords:
- 你 (反汇编实模式下 BIOS) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ur (Unassemble Real Mode BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5922e23340d416f45f37fa88917f8e20afe7322e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522007"
---
# <a name="ur-unassemble-real-mode-bios"></a>你 (反汇编实模式下 BIOS)


**你**命令显示指定的 16 位实模式代码程序集转换。

```dbgcmd
ur Range 
ur Address
ur 
```

## <a name="span-idddkcmdunassemblerealmodebiosdbgspanspan-idddkcmdunassemblerealmodebiosdbgspanparameters"></a><span id="ddk_cmd_unassemble_real_mode_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_REAL_MODE_BIOS_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定包含要拆装的说明进行操作的内存范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要拆装的内存范围的起始时间。 未组装的八个的说明 （基于 x86 处理器） 或 （在基于 Itanium 处理器上） 的九个说明。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何调试 BIOS 代码的详细信息，请参阅[调试 BIOS 代码](debugging-bios-code.md)。

<a name="remarks"></a>备注
-------

如果未指定*范围*或*地址*，反汇编当前地址处开始并扩展了八个的说明 （基于 x86 处理器） 或 （在基于 Itanium 处理器上） 的九个说明。

如果你正在检查 16 位实模式代码在基于 x86 的处理器上，同时**你**命令和[ **u （反汇编）** ](u--unassemble-.md)命令提供正确的结果。

但是，如果在调试程序不是的位置存在实模式代码应为它 （例如，非 x86 或的计算机是运行模拟以插件卡从基于 x86 的 BIOS 代码），则必须使用**你**正确反汇编这代码。

如果您使用**你**命令尝试在 32 位或 64 位代码中，反汇编代码，就好像 16 位代码。 这种情况下会产生无意义的结果。

 

 





