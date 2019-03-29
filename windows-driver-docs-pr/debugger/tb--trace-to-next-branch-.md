---
title: tb（跟踪到下一个分支）
description: Tb 命令执行程序，直到达到分支指令。
ms.assetid: 28b736f9-69f5-405b-9684-48b4205e7633
keywords:
- tb （跟踪到下一个分支） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tb (Trace to Next Branch)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c32e3f437b69aa4d04a0dfdfa4e2fce141d5a3e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562577"
---
# <a name="tb-trace-to-next-branch"></a>tb（跟踪到下一个分支）


**Tb**命令执行程序，直到达到分支指令。

```dbgcmd
tb [r] [= StartAddress] [Count] 
```

## <a name="span-idddkcmdtracetonextbranchdbgspanspan-idddkcmdtracetonextbranchdbgspanparameters"></a><span id="ddk_cmd_trace_to_next_branch_dbg"></span><span id="DDK_CMD_TRACE_TO_NEXT_BRANCH_DBG"></span>参数


<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**tbr**， [ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 所有这些命令控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他四个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定的分支，以允许的数目。 遇到分支时，每次指令地址和该指令将显示。 如果省略*计数*，默认数量为 1。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p></p>
<strong>基于 x86 的：</strong>内核模式下<strong>基于 Itanium 的：</strong>用户模式下，内核模式<strong>基于 x64 的：</strong>用户模式下，内核模式</td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 的 （GenuineIntel 处理器系列 6 及更高版本），基于 Itanium 的、 基于 x64</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Tb**命令将导致目标开始执行。 此执行继续，直到达到分支命令。

在未采取任何分支命令处停止执行。 执行此停止始终基于*反汇编*代码，即使在调试器处于源模式。

分支指令包括的调用，返回、 跳转，计数循环，和 while 循环。 如果调试器遇到无条件分支或条件分支条件为 true，执行将停止。 如果调试器遇到条件分支条件为 false，则继续执行。

当执行停止时，会显示分支指令和任何关联的符号的地址。 此信息后跟一个箭头，然后地址和新的程序计数器位置的说明。

**Tb**命令仅适用于当前的处理器。 如果您使用**tb**在多处理器系统上，执行停止时达到分支命令或另一个处理器的事件发生时，具体取决于第一个。

通常情况下，处理器控制块 (PRCB) 初始化后启用分支跟踪。 （PRCB 初始化在启动过程中尽早中）。但是，如果您必须使用**tb**可以使用此点之前命令[ **.force\_tb （允许分支的跟踪强行）** ](-force-tb--forcibly-allow-branch-tracing-.md)启用分支跟踪前面。 使用 **.force\_tb**命令谨慎，因为它可能会损坏处理器状态。

 

 





