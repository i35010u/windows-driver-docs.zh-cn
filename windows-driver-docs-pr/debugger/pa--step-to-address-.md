---
title: pa （到地址的步骤）
description: Pa 命令执行程序，直到达到指定的地址时，显示每个步骤。
ms.assetid: 497261a9-69fb-4df2-b342-cd62bda8a51f
keywords:
- pa （到地址的步骤） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pa (Step to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b00bb0951cb306f538499ea35fa52504121321d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526895"
---
# <a name="pa-step-to-address"></a>pa （到地址的步骤）


**Pa**命令执行程序，直到达到指定的地址时，显示每个步骤。

User-Mode

```dbgcmd
[~Thread] pa [r] [= StartAddress] StopAddress ["Command"]
```

Kernel-Mode

```dbgcmd
pa [r] [= StartAddress] StopAddress ["Command"]
```

## <a name="span-idddkcmdsteptoaddressdbgspanspan-idddkcmdsteptoaddressdbgspanparameters"></a><span id="ddk_cmd_step_to_address_dbg"></span><span id="DDK_CMD_STEP_TO_ADDRESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定线程继续执行。 所有其他线程均已冻结。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**par**， [ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 所有这些命令控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他三个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 否则，调试器在指令指针指向的指令开始。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span> *StopAddress*   
指定将停止执行的地址。 此地址必须与匹配确切的地址的指令。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定要执行后执行步骤的调试器命令。 标准之前执行此命令**pa**显示结果。 如果还使用*StopAddress*，指定的命令执行后*StopAddress*达到 （但之前的最后一步的结果会显示）。

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

有关相关命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Pa**命令将导致目标开始执行。 此执行继续，直到达到指定的指令或遇到断点。

**请注意**  任何虚拟地址空间中指定的虚拟地址处遇到一条指令时，如果在内核模式下使用此命令，停止执行。

 

在此执行期间将显式显示的所有步骤。 调用的函数被视为单个单元。 因此，此命令显示的是与你看到是否您执行类似[ **p （步骤）** ](p--step-.md)重复直到程序计数器达到指定的地址。

例如，以下命令显式将逐步指导目标代码直到到达当前函数的返回地址。

```dbgcmd
0:000> pa @$ra 
```

下面的示例演示了如何使用**pa**命令连同**kb**命令以显示堆栈跟踪：

```dbgcmd
0:000> pa 70b5d2f1 "kb"
```

 

 





