---
title: p（步进）
description: P 命令执行单个指令或源行，并有选择性地显示所有寄存器和标志的生成值。
ms.assetid: 4ee24e76-b751-4346-80af-d481d9513ce0
keywords:
- p （步骤） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- p (Step)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cac8b8f3578104ecf07d0ed4150b77b6e2d22e00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351475"
---
# <a name="p-step"></a>p（步进）


**P**命令执行单个指令或源行，并有选择性地显示所有寄存器和标志的生成值。 当子例程调用或中断发生，它们被视为单步执行。

User-Mode

```dbgcmd
[~Thread] p[r] [= StartAddress] [Count] ["Command"] 
```

Kernel-Mode

```dbgcmd
p[r] [= StartAddress] [Count] ["Command"] 
```

## <a name="span-idddkcmdstepdbgspanspan-idddkcmdstepdbgspanparameters"></a><span id="ddk_cmd_step_dbg"></span><span id="DDK_CMD_STEP_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定的线程继续执行。 所有其他线程均已冻结。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**pr**， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 这些命令的所有三个控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他三个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定应开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定说明或源行之前停止单步执行的数。 在独立的方式显示每个步骤[调试器命令窗口](debugger-command-window.md)。 默认值为 1。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定要执行后执行步骤的调试器命令。 标准之前执行此命令**p**显示结果。 如果还使用*计数*，指定的命令执行所有单步执行完毕后 （但之前的最后一步的结果会显示）。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

详细了解颁发**p**相关命令的命令和的概述，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

当指定*计数*，将显示每个指令，如通过单步执行。

如果调试器遇到**调用**指令或中断时单步执行，被调用的子例程将执行完全除非遇到断点。 控制权返回给调试器在调用或中断之后的下一个指令。

每个步骤执行的单个程序集指令或单个源行，具体取决于调试器是否在程序集模式或源模式中。 使用[ **l + t** ](l---l---set-source-options-.md)和 l-t 命令或 WinDbg 工具栏上的按钮这些模式之间切换。

时快速中 WinDbg 中逐步执行很多时候，每个步骤后更新了调试窗口中的信息。 如果此更新将导致速度较慢的响应时间，使用[ **.suspend\_ui （挂起 WinDbg 界面）** ](-suspend-ui--suspend-windbg-interface-.md)以暂时挂起这些窗口的刷新。

 

 





