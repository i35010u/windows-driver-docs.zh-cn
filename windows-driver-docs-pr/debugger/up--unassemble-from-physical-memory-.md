---
title: 向上 （从物理内存的反汇编）
description: 最命令显示指定的程序代码程序集转换物理内存中。
ms.assetid: 4db66566-b7b8-4f1e-9492-b4b78016b45a
keywords:
- 向上 （从物理内存的反汇编） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- up (Unassemble from Physical Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bceebc2d2b5969f9d5631bbab5e5740882220b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555736"
---
# <a name="up-unassemble-from-physical-memory"></a>向上 （从物理内存的反汇编）


**向上**命令显示指定的程序代码程序集转换的物理内存中。

```dbgcmd
up Range 
up Address 
up 
```

## <a name="span-idddkcmdunassembledbgspanspan-idddkcmdunassembledbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定包含要拆装的说明进行操作的物理内存中的内存范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
中的物理内存来反汇编指定的内存范围的开头。 未组装的八个的说明 （基于 x86 处理器） 或 （在基于 Itanium 处理器上） 的九个说明。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

调试和相关命令，请参阅有关程序集的详细信息[在程序集模式下调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果未指定的参数**向上**命令中，反汇编的当前地址处开始并扩展了八个的说明 （基于 x86 处理器） 或 （在基于 Itanium 处理器上） 的九个指令。

不要将使用此命令相混淆[ **u （反汇编）**](u--unassemble-.md)。 **向上**命令反汇编仅物理内存，而**u**命令反汇编仅虚拟内存。

 

 





