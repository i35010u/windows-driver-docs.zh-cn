---
title: tb（跟踪到下一个分支）
description: 在到达分支指令之前，tb 命令会执行程序。
ms.assetid: 28b736f9-69f5-405b-9684-48b4205e7633
keywords:
- tb (跟踪到下一个分支) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tb (Trace to Next Branch)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f24ea77dcbf4adbf08af8f30ebaa90dd14df5a3f
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148389"
---
# <a name="tb-trace-to-next-branch"></a>tb（跟踪到下一个分支）


在到达分支指令之前， **tb**命令会执行程序。

```dbgcmd
tb [r] [= StartAddress] [Count] 
```

## <a name="span-idddk_cmd_trace_to_next_branch_dbgspanspan-idddk_cmd_trace_to_next_branch_dbgspanparameters"></a><span id="ddk_cmd_trace_to_next_branch_dbg"></span><span id="DDK_CMD_TRACE_TO_NEXT_BRANCH_DBG"></span>参数


<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以使用**tbr**、 [**pr**](p--step-.md)、 [**tr**](t--trace-.md)或提示 \_ 允许-reg 命令禁用注册显示。 所有这些命令都控制相同的设置，你可以使用其中任何一个命令来替代以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他四个命令不同。 若要控制显示哪些寄存器和标志，请使用[**rm (注册掩码) **](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 如果不使用*StartAddress*，则将从指令指针指向的指令开始执行。 有关语法的详细信息，请参阅[address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定允许的分支数。 每次遇到分支时，都会显示说明地址和指令。 如果省略*Count*，则默认数字为1。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p></p>
<strong>基于 x86：</strong>内核模式<strong>：仅基于 x64：</strong>用户模式，内核模式</td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 的 (GenuineIntel 处理器系列6和更高版本) ，基于 x64</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Tb**命令导致目标开始执行。 此执行将继续，直到到达分支命令。

执行在任何要执行的分支命令处停止。 此停止执行始终基于*反汇编*代码，即使调试器处于源模式下也是如此。

分支指令包括调用、返回、跳转、计数循环和 while 循环。 如果调试器遇到无条件分支或条件为 true 的条件分支，将停止执行。 如果调试器遇到条件为 false 的条件分支，将继续执行。

当执行停止时，将显示分支指令的地址以及任何关联的符号。 此信息后跟一个箭头，然后是新程序计数器位置的地址和说明。

**Tb**命令仅适用于当前处理器。 如果在多处理器系统上使用**tb** ，则在到达分支命令或发生另一个处理器事件时将停止执行（以先达到的条件为准）。

通常，在初始化了处理器控制块 (PRCB) 后，会启用分支跟踪。  (在启动过程的早期初始化 PRCB。 ) 不过，如果在此之前必须使用**tb**命令，则可以使用[**。 Force \_ Tb (强制允许分支跟踪) **](-force-tb--forcibly-allow-branch-tracing-.md) ，以便之前启用分支跟踪。 请谨慎使用**force \_ tb**命令，因为它可能会损坏处理器状态。

 

 





