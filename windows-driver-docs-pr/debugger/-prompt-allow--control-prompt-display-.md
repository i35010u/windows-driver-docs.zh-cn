---
title: .prompt_allow（控制提示显示）
description: .Prompt_allow 命令控制在单步执行和跟踪期间显示的信息以及目标的执行停止的时间。
keywords:
- .prompt_allow (控件提示显示) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .prompt_allow (Control Prompt Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9a7e5167bca7df17c060c79be1acf9319b84f16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837593"
---
# <a name="prompt_allow-control-prompt-display"></a>。 prompt \_ 允许 (控件提示显示) 


**Prompt \_ allow** 命令控制在单步执行和跟踪期间显示的信息以及目标的执行停止的时间。

```dbgcmd
.prompt_allow {+|-}Item [...] 
.prompt_allow 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="______________"></span> **+**   
显示单步执行、跟踪和执行提示处的指定项。 必须在加号 (+) 之前添加一个空格，但不能在其后面添加一个空格。

<span id="_______-______"></span> **-**   
阻止在单步执行、跟踪和执行提示符下显示指定项。 你必须在减号 ( ) 之前添加一个空格，但不能在其后面添加一个空格。

<span id="_______Item______"></span><span id="_______item______"></span><span id="_______ITEM______"></span>*项*   
指定要显示或不显示的项。 可以指定任意数量的项。 用空格分隔多个项。 必须在每个项之前添加加号 (+) 或减号 ( ) 。 你可以使用以下项：

<span id="dis"></span><span id="DIS"></span>**取消它**  
当前位置的反汇编说明。

<span id="ea"></span><span id="EA"></span>**中文**  
当前指令的有效地址。

<span id="reg"></span><span id="REG"></span>**本文**  
最重要的寄存器的当前状态。 您可以使用 [**pr**](p--step-.md)、 [**tr**](t--trace-.md)或提示禁止注册显示 \_ 。 这三个命令都控制相同的设置，您可以使用它们中的任何一个来覆盖以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他三个命令分开，如下面的 "备注" 部分所述。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="src"></span><span id="SRC"></span>**源**  
与当前指令相对应的源行。 您可以使用 l-ls 或 prompt \_ allow-src; 命令禁用源行显示。 必须通过这两种机制来使源行显示可见。

<span id="sym"></span><span id="SYM"></span>**符号**  
当前指令的符号。 此符号包括当前模块、函数名称和偏移量。

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
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关影响执行的命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

您可以使用 **。 prompt 不 \_** 带参数的命令，以显示哪些项已显示并且未显示。 每 **次运行时 \_**，调试器都只更改指定项的状态。

默认情况下，将显示所有项。

如果使用了 l + os 选项，此选项将覆盖除 **src** 之外的 **\_ 任何选项。**

你还可以使用复杂的命令，如以下示例。

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

 

 





