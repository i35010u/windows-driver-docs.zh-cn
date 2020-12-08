---
title: t（跟踪）
description: T 命令执行单个指令或源行，并选择性地显示所有寄存器和标志的结果值。
keywords:
- t (跟踪) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- t (Trace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e55b1db32003b0d31a140edcc538ea3745f3b93e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833163"
---
# <a name="t-trace"></a>t（跟踪）


**T** 命令执行单个指令或源行，并选择性地显示所有寄存器和标志的结果值。 当发生子程序调用或中断时，也会跟踪其每个步骤。

User-Mode

```dbgcmd
[~Thread] t [r] [= StartAddress] [Count] ["Command"] 
```

Kernel-Mode

```dbgcmd
t [r] [= StartAddress] [Count] ["Command"] 
```

## <a name="span-idddk_cmd_trace_dbgspanspan-idddk_cmd_trace_dbgspanparameters"></a><span id="ddk_cmd_trace_dbg"></span><span id="DDK_CMD_TRACE_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要解冻的线程。 所有其他线程均已冻结。 有关此语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以使用 [**pr**](p--step-.md)、 **tr** 或提示禁止注册显示 \_ 。 这三个命令都控制同一个设置，你可以使用其中任何一个命令来覆盖以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他三个命令不同。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定应开始执行的地址。 如果不使用 *StartAddress*，则将从指令指针指向的指令开始执行。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定在停止之前要跟踪的指令或源行的数目。 每个步骤都在 [调试器命令窗口](debugger-command-window.md)中显示为单独的操作。 默认值为一。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
指定执行跟踪后要执行的调试器命令。 此命令在显示标准 **t** 结果之前执行。 如果还使用 *Count*，则在所有跟踪都完成后 (，但在最终跟踪的结果显示) 之前，将执行此命令。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何发出 **t** 命令和相关命令的概述的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

指定 *计数* 时，每个指令的显示方式均为单步执行。

每个跟踪都执行单个程序集指令或单个源行，具体取决于调试器是处于程序集模式还是源模式。 使用 " [**+ t**](l---l---set-source-options-.md) " 和 "l t" 命令，或使用 WinDbg 工具栏上的按钮在这两种模式之间切换。

如果要跟踪大部分函数调用，但跳过某些调用，则可以使用 [**。步骤 \_ 筛选器 (设置步骤筛选器)**](-step-filter--set-step-filter-.md) ，以指示要逐过程进行的调用。

可以使用 **t** 命令来跟踪 ROM 中的指令。

如果在 WinDbg 中快速跟踪多次，则每次跟踪后都会更新调试信息窗口。 如果此更新导致响应时间变慢，请使用 [**。暂停 \_ Ui (挂起 WinDbg 接口)**](-suspend-ui--suspend-windbg-interface-.md) 以暂时挂起这些 windows 的更新。

 

 





