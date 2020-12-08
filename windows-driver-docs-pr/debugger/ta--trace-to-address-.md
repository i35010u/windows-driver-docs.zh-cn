---
title: ta（跟踪到地址）
description: Ta 命令执行程序，直到达到指定的地址，并显示每个步骤 (包括) 调用的函数中的步骤。
keywords:
- ta (跟踪) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ta (Trace to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 424e4911a9b3e68736b1bededb24e840e382893b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833159"
---
# <a name="ta-trace-to-address"></a>ta（跟踪到地址）


**Ta** 命令执行程序，直到达到指定的地址，并显示每个步骤 (包括) 调用的函数中的步骤。

User-Mode

```dbgcmd
[~Thread] ta [r] [= StartAddress] StopAddress 
```

Kernel-Mode

```dbgcmd
ta [r] [= StartAddress] StopAddress 
```

## <a name="span-idddk_cmd_trace_to_address_dbgspanspan-idddk_cmd_trace_to_address_dbgspanparameters"></a><span id="ddk_cmd_trace_to_address_dbg"></span><span id="DDK_CMD_TRACE_TO_ADDRESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要继续执行的线程。 所有其他线程均已冻结。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以通过使用 **tar**、 [**pr**](p--step-.md)、 [**tr**](t--trace-.md)或提示禁止注册显示 \_ 。 所有这些命令都控制相同的设置，并且使用其中任何一个都将替代以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他四个命令不同。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 如果不使用 *StartAddress*，则将从指令指针指向的指令开始执行。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span>*StopAddress*   
指定执行停止的地址。 此地址必须与指令的确切地址匹配。

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

**Ta** 命令导致目标开始执行。 此执行将继续，直到到达指定的指令或遇到断点。

**注意**   如果在内核模式下使用 **ta** 命令，则在任何虚拟地址空间中的指定虚拟地址处遇到指令时，将停止执行。

 

在此执行过程中，将显式显示所有步骤。 如果调用了函数，则调试器还会通过该函数进行跟踪。 因此，此命令的显示内容与你在 [**(跟踪)**](t--trace-.md) 重复执行时显示的内容类似，直到程序计数器到达指定的地址。

例如，以下命令将显式跟踪目标代码，直到达到当前函数的返回地址。

```dbgcmd
0:000> ta @$ra 
```

 

 





