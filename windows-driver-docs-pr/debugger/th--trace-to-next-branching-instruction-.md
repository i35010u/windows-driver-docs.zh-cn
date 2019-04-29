---
title: th（跟踪到下一个分支指令）
description: Th 命令执行程序，直到它达到包括条件分支指令的任何类型或无条件分支，调用返回，并且系统调用。
ms.assetid: 42b7ceb6-c507-45b3-9186-0a4014b68a28
keywords:
- 日 （到下一步的分支指令的跟踪） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- th (Trace to Next Branching Instruction)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e3eb9dcfc2b3018c2735518250b814e02d5f7e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364719"
---
# <a name="th-trace-to-next-branching-instruction"></a>th（跟踪到下一个分支指令）


**Th**命令执行程序，直到它达到包括条件分支指令的任何类型或无条件分支，调用返回，并且系统调用。

User-Mode

```dbgcmd
[~Thread] th [r] [= StartAddress] [Count] 
```

Kernel-Mode

```dbgcmd
th [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定线程继续执行。 所有其他线程均已冻结。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
开启和关闭显示器的寄存器和标志。 默认情况下，显示的寄存器和标志。 可以使用禁用注册显示**对**， [ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 所有这些命令控制的相同设置，可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他四个命令。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定调试器必须用于遇到的分支指令数**th**命令以结束。 默认值为 1。

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

**Th**命令将导致目标开始执行。 执行将继续直至调试器到达分支指令或遇到断点。

如果程序计数器已在分支指令上，调试器将跟踪为分支指令，并继续执行，直至到达另一个分支指令。 此跟踪，而不是执行中的，在调用之间的唯一区别是**th**并[ **p h （到下一个分支指令的步骤）**](ph--step-to-next-branching-instruction-.md)。

**th**是可用的所有实时会话。 此可用性之间的主要区别是**th**并[ **tb （跟踪到下一个分支）**](tb--trace-to-next-branch-.md)。

在源模式中，可以将一个源行与多个程序集指令相关联。 此命令不会停止在当前的源行与相关联的分支指令。

 

 





