---
title: up（从物理内存取消汇编）
description: Up 命令显示物理内存中指定程序代码的程序集转换。
ms.assetid: 4db66566-b7b8-4f1e-9492-b4b78016b45a
keywords:
- ) Windows 调试，从物理内存向上 (Unassemble
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- up (Unassemble from Physical Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72f6e13b0e890802dbf36aaf43f944ccbb42599d
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148369"
---
# <a name="up-unassemble-from-physical-memory"></a>up（从物理内存取消汇编）


**Up**命令显示物理内存中指定程序代码的程序集转换。

```dbgcmd
up Range 
up Address 
up 
```

## <a name="span-idddk_cmd_unassemble_dbgspanspan-idddk_cmd_unassemble_dbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定物理内存中包含要拆卸的指令的内存范围。 有关语法的详细信息，请参阅[address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定物理内存中要拆装的内存范围的开始位置。 基于 x86 的处理器上的八个说明是 unassembled 的。 有关语法的详细信息，请参阅[address 和 Address Range 语法](address-and-address-range-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的详细信息，请参阅[程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果没有为**up**命令指定参数，则反汇编将从当前地址开始，并在基于 x86 的处理器上扩展八个指令。

请勿将此命令与[**u (Unassemble) **](u--unassemble-.md)混淆。 **Up**命令只反汇编物理内存，而**u**命令只反汇编虚拟内存。

 

 





