---
title: u，ub，uu （反汇编）
description: U * 命令在内存中将显示指定的程序代码的程序集翻译。 此命令不应混淆和 ~ u （取消冻结线程） 命令。
ms.assetid: 933a308c-61d1-4ca4-89c1-5749ba1b41c1
keywords:
- u、 ub、 uu （反汇编） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- u, ub, uu (Unassemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4e70cbe647cfb76cddcff3baa9e6669d1684904
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380778"
---
# <a name="u-ub-uu-unassemble"></a>u，ub，uu （反汇编）


**U\\*** 命令显示指定的程序代码程序集转换在内存中。

不要将此命令使用相混淆[ **~ （取消冻结线程） 的 u** ](-u--unfreeze-thread-.md)命令。

```dbgcmd
u[u|b] Range 
u[u|b] Address
u[u|b] 
```

## <a name="span-idddkcmdunassembledbgspanspan-idddkcmdunassembledbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定包含要拆装的说明进行操作的内存范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。 如果您使用**b**标志，则必须指定*范围*通过使用"*地址* **L * * * 长度*"语法、 不"*地址 1 Address2*"语法。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要拆装的内存范围的起始时间。 未组装的八个的说明 （基于 x86 处理器） 或 （在基于 Itanium 处理器上） 的九个说明。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______b______"></span><span id="_______B______"></span> **b**   
确定要拆装的方法是计算向后的内存范围。 如果**ub** *地址*是使用，则已拆装的期将为八个或九个字节范围结尾*地址*。 如果使用语法指定一系列**ub** *地址* **L * * * 长度*，已拆装的范围为结束时间指定长度的范围*地址*。

<span id="_______u______"></span><span id="_______U______"></span> **u**   
指定即使没有内存读取错误反汇编会继续运行。

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

如果未指定的参数**u**命令中，反汇编的当前地址处开始并扩展了八个的说明 （基于 x86 或基于 x64 的处理器） 或 （在基于 Itanium 处理器上） 的九个指令。 当你使用**ub**反汇编不带参数，包括当前地址前的八个或九个说明。

不要将使用此命令相混淆[ **（从物理内存的反汇编） 向上**](up--unassemble-from-physical-memory-.md)。 **U**命令反汇编仅虚拟内存，而**向上**命令反汇编仅物理内存。

 

 





