---
title: u、ub、uu (Unassemble)
description: U * 命令显示内存中指定程序代码的程序集转换。 不应将此命令与 ~ u (解冻线程) 命令混淆。
ms.assetid: 933a308c-61d1-4ca4-89c1-5749ba1b41c1
keywords:
- u、ub、uu (Unassemble) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- u, ub, uu (Unassemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b0931b1ff3ef4b7a3be6f97b948edf44d2808a0
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866763"
---
# <a name="u-ub-uu-unassemble"></a>u、ub、uu (Unassemble)


**U\\** * 命令显示内存中指定程序代码的程序集转换。

不应将此命令与[ **~ u (解冻线程)** ](-u--unfreeze-thread-.md)命令混淆。

```dbgcmd
u[u|b] Range 
u[u|b] Address
u[u|b] 
```

## <a name="span-idddk_cmd_unassemble_dbgspanspan-idddk_cmd_unassemble_dbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>Parameters


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定包含要拆装的指令的内存范围。 有关语法的详细信息, 请参阅[address 和 Address Range 语法](address-and-address-range-syntax.md)。 如果使用**b**标志, 则必须使用 "*Address* **L**_Length_" 语法而不是 "1-1 地址*2*" 语法指定*范围*。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要反汇编的内存范围的开始位置。 8个说明 (在基于 x86 的处理器上) 或9个说明 (在基于 Itanium 的处理器上) 是 unassembled。 有关语法的详细信息, 请参阅[address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______b______"></span><span id="_______B______"></span>**b**   
通过倒计时确定要拆卸的内存范围。 如果使用了**ub** *Address* , 则反汇编范围将是以*Address*结尾的八个或9个字节范围。 如果使用语法**ub** *Address* **L**_Length_指定范围, 则反汇编范围将为指定长度的范围, 以*地址*结束。

<span id="_______u______"></span><span id="_______U______"></span>**u**   
指定即使出现内存读取错误, 反汇编仍将继续。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式, 内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时, 故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的详细信息, 请参阅[程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果未指定**u**命令的参数, 则反汇编将从当前地址开始, 并扩展八个指令 (在基于 x86 或基于 x64 的处理器上) 或9个说明 (在基于 Itanium 的处理器上)。 如果使用不带参数的**ub** , 则反汇编会在当前地址之前包含八个或九个指令。

不要将此命令与[**up (Unassemble 从物理内存)** ](up--unassemble-from-physical-memory-.md)混淆。 **U**命令仅反汇编虚拟内存, 而**up**命令只反汇编物理内存。

 

 





