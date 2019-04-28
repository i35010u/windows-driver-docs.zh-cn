---
title: t（跟踪）
description: T 命令执行单个指令或源行，并有选择性地显示所有寄存器和标志的生成值。
ms.assetid: 0cb3ac96-5d5c-4ebd-8ef1-2fbb066e6458
keywords:
- t (Trace) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- t (Trace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d2cd6116ac3d69a4e5c8c0076c699a4fd6b452e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335456"
---
# <a name="t-trace"></a>t（跟踪）


**T**命令执行单个指令或源行，并有选择性地显示所有寄存器和标志的生成值。 当出现子例程调用或中断，也将他们执行的步骤的每个被跟踪。

User-Mode

```dbgcmd
[~Thread] t [r] [= StartAddress] [Count] ["Command"] 
```

Kernel-Mode

```dbgcmd
t [r] [= StartAddress] [Count] ["Command"] 
```

## <a name="span-idddkcmdtracedbgspanspan-idddkcmdtracedbgspanparameters"></a><span id="ddk_cmd_trace_dbg"></span><span id="DDK_CMD_TRACE_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定解冻线程。 所有其他线程均已冻结。 有关此语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示[ **pr**](p--step-.md)， **tr**，或.prompt\_允许-reg 命令。 这些命令的所有三个控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他三个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定应开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定说明或通过停止前的跟踪源行的号。 在独立的方式显示每个步骤[调试器命令窗口](debugger-command-window.md)。 默认值为 1。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定要执行后执行跟踪的调试器命令。 标准之前执行此命令**t**显示结果。 如果还使用*计数*，此命令执行的所有跟踪完成后 （但才会显示最终的跟踪的结果）。

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

详细了解如何发出**t**相关命令的命令和的概述，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

当指定*计数*，将显示每个指令，如通过单步执行。

每个跟踪的单个程序集指令或单个源行，具体取决于调试器是否在程序集模式或源模式中执行。 使用[ **l + t** ](l---l---set-source-options-.md)和 l-t 命令或 WinDbg 工具栏上的按钮这些模式之间切换。

如果你想要跟踪大多数函数调用，但跳过某些调用，则可以使用[**步骤\_筛选器 （设置步骤筛选器）** ](-step-filter--set-step-filter-.md)以指示它通过调用到步骤。

可以使用**t**命令跟踪文档中的说明 rom。

当在 WinDbg 中，快速跟踪很多时候时，调试窗口中的信息进行更新后每个跟踪。 如果此更新将导致速度较慢的响应时间，使用[ **.suspend\_ui （挂起 WinDbg 界面）** ](-suspend-ui--suspend-windbg-interface-.md)以暂时挂起更新这些窗口。

 

 





