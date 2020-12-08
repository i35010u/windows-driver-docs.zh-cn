---
title: pa（步进到地址）
description: Pa 命令执行程序，直到达到指定的地址，并显示每个步骤。
keywords:
- pa (解决) Windows 调试的步骤
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pa (Step to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5941d4d3f2dea90b768306f0a243d90d4f43a4e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819153"
---
# <a name="pa-step-to-address"></a>pa（步进到地址）


**Pa** 命令执行程序，直到达到指定的地址，并显示每个步骤。

User-Mode

```dbgcmd
[~Thread] pa [r] [= StartAddress] StopAddress ["Command"]
```

Kernel-Mode

```dbgcmd
pa [r] [= StartAddress] StopAddress ["Command"]
```

## <a name="span-idddk_cmd_step_to_address_dbgspanspan-idddk_cmd_step_to_address_dbgspanparameters"></a><span id="ddk_cmd_step_to_address_dbg"></span><span id="DDK_CMD_STEP_TO_ADDRESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要继续执行的线程。 所有其他线程均已冻结。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以通过使用 " **par**， [**pr**](p--step-.md)， [**tr**](t--trace-.md)" 或 "prompt \_ 允许-reg" 命令禁用注册显示。 所有这些命令都控制相同的设置，你可以使用其中任何一个命令来替代以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他三个命令不同。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 否则，调试器会从指令指针指向的指令开始。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span>*StopAddress*   
指定将停止执行的地址。 此地址必须与指令的确切地址匹配。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
指定执行步骤之后要执行的调试器命令。 此命令在显示标准 **pa** 结果之前执行。 如果还使用 *StopAddress*， *则在)* (上，然后在最后一个步骤的结果显示之前，将执行指定的命令。

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

有关相关命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Pa** 命令导致目标开始执行。 此执行将继续，直到到达指定的指令或遇到断点。

**注意**   如果在内核模式下使用此命令，则在任何虚拟地址空间中的指定虚拟地址处遇到指令时，将停止执行。

 

在此执行过程中，将显式显示所有步骤。 被调用的函数被视为单个单元。 因此，此命令的显示内容与您在执行 [**p (步骤)**](p--step-.md) 时所看到的内容相似，直到程序计数器到达指定的地址。

例如，以下命令将显式逐句通过目标代码，直到达到当前函数的返回地址。

```dbgcmd
0:000> pa @$ra 
```

下面的示例演示如何结合使用 **pa** 命令和 **kb** 命令来显示堆栈跟踪：

```dbgcmd
0:000> pa 70b5d2f1 "kb"
```

 

 





