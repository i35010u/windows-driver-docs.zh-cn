---
title: ta（跟踪到地址）
description: Ta 命令执行程序直至达到指定的地址，显示每个步骤 （包括调用的函数中的步骤）。
ms.assetid: 99741659-dd43-44ea-ac27-06d821b47fbe
keywords:
- ta （跟踪到地址） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ta (Trace to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fda2fbf6e537c8b88a0fb9349da4a942791ec88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368011"
---
# <a name="ta-trace-to-address"></a>ta（跟踪到地址）


**Ta**命令执行程序，直到达到指定的地址时，显示每个步骤 （包括调用的函数中的步骤）。

User-Mode

```dbgcmd
[~Thread] ta [r] [= StartAddress] StopAddress 
```

Kernel-Mode

```dbgcmd
ta [r] [= StartAddress] StopAddress 
```

## <a name="span-idddkcmdtracetoaddressdbgspanspan-idddkcmdtracetoaddressdbgspanparameters"></a><span id="ddk_cmd_trace_to_address_dbg"></span><span id="DDK_CMD_TRACE_TO_ADDRESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定线程继续执行。 所有其他线程均已冻结。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**tar**， [ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 所有这些命令控制的相同设置，并使用其中任何一个将覆盖任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他四个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span> *StopAddress*   
指定在执行停止的地址。 此地址必须与匹配确切的地址的指令。

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

**Ta**命令将导致目标开始执行。 此执行继续，直到达到指定的指令或遇到断点。

**请注意**  如果你使用**ta**在内核模式下，任何虚拟地址空间中指定的虚拟地址处遇到一条指令时停止执行命令。

 

在此执行期间将显式显示的所有步骤。 如果调用的函数，则调试器还会跟踪通过该功能。 因此，此命令显示类似于如果执行了您看到的内容[ **t (Trace)** ](t--trace-.md)重复直至程序计数器达到指定的地址。

例如，以下命令显式跟踪通过目标代码直到到达当前函数的返回地址。

```dbgcmd
0:000> ta @$ra 
```

 

 





