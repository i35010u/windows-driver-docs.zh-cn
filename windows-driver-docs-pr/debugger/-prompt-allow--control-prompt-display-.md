---
title: .prompt_allow（控制提示显示）
description: .Prompt_allow 命令控件在单步执行和跟踪和目标的执行停止时显示的信息。
ms.assetid: 916114f9-0a68-4423-ba28-a5f0da8a1af9
keywords:
- .prompt_allow （控制提示显示） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .prompt_allow (Control Prompt Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec4492e245bdefabab5643f182e06b72cc0371a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565953"
---
# <a name="promptallow-control-prompt-display"></a>.prompt\_允许 （控制提示显示）


**.Prompt\_允许**命令期间单步执行和跟踪和目标的执行停止时显示的信息的控件。

```dbgcmd
.prompt_allow {+|-}Item [...] 
.prompt_allow 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="______________"></span> **+**   
在单步执行、 跟踪和执行提示符显示指定的项。 您必须添加加号 （+） 之前的空格，但不能在其后添加一个空格。

<span id="_______-______"></span> **-**   
阻止在单步执行、 跟踪和执行提示符显示指定的项。 您必须添加减号 （-） 之前的空格，但不能在其后添加一个空格。

<span id="_______Item______"></span><span id="_______item______"></span><span id="_______ITEM______"></span> *Item*   
指定要显示或隐藏的项。 可以指定任意数量的项。 分隔多个项由空格。 必须添加加号 （+） 或每个项前的减号 （-）。 可以使用以下各项：

<span id="dis"></span><span id="DIS"></span>**dis**  
在当前位置已拆装的说明。

<span id="ea"></span><span id="EA"></span>**ea**  
当前指令有效地址。

<span id="reg"></span><span id="REG"></span>**reg**  
最重要的寄存器的当前状态。 可以使用禁用注册显示[ **pr**](p--step-.md)， [ **tr**](t--trace-.md)，或.prompt\_允许-reg 命令。 这些命令的所有三个控制相同设置，并且可以使用其中任何一个重写任何以前使用这些命令。

此外可以使用 l os 命令来禁用注册显示。 此设置是独立于其他的三个命令，如下面的备注部分中所述。 控制要显示的寄存器和标志，使用[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="src"></span><span id="SRC"></span>**src**  
当前指令对应的源代码行。 可以通过使用 l ls 或.prompt 禁用源代码行显示\_允许-src; 命令。 通过显示这两种机制，必须启用源行显示。

<span id="sym"></span><span id="SYM"></span>**sym**  
当前指令的符号。 此符号包括当前模块、 函数名称和偏移量。

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
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关影响执行命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

可以使用 **.prompt\_允许**命令不带参数，表明哪些项显示，但不显示。 每次你运行 **.prompt\_允许**，调试器会将指定的项状态更改。

默认情况下，显示所有项。

如果你已使用 l + os 选项，此选项将重写任一 **.prompt\_允许**选项而不**src**。

此外可以使用复杂的命令，如下面的示例。

```dbgcmd
0:000> .prompt_allow -reg -dis +ea 
Allow the following information to be displayed at the prompt:
(Other settings can affect whether the information is actually displayed)
   sym - Symbol for current instruction
    ea - Effective address for current instruction
   src - Source info for current instruction
Do not allow the following information to be displayed at the prompt:
   dis - Disassembly of current instruction
   reg - Register state
```

 

 





