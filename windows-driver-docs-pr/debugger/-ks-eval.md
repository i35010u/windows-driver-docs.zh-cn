---
title: ks.eval
description: Ks.eval 扩展计算表达式中使用的特定于扩展的表达式计算器。
ms.assetid: 68c9cfb0-ff87-47ea-bd0d-5f45c1de0639
keywords:
- ks.eval Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.eval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e5c02094509d424108666be077921e1daebc424
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519855"
---
# <a name="kseval"></a>!ks.eval


**！ Ks.eval**扩展的计算结果表达式中使用的特定于扩展的表达式计算器。

```dbgcmd
!ks.eval Expression 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要计算的表达式。 *表达式*可以包含任何 MASM 运算符、 符号或数字语法，以及下面所述的特定于扩展的运算符。 MASM 表达式的详细信息，请参阅[MASM 数字和运算符](masm-numbers-and-operators.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

扩展模块地址参数扩展命令中包括可用于两个特定于扩展的运算符：

<span id="________fdo_________x_________"></span><span id="________FDO_________X_________"></span> **fdo(** *x* **)**  
返回与地址处的对象关联的功能的设备对象**x**。

<span id="________driver_________x_________"></span><span id="________DRIVER_________X_________"></span> **driver(** *x* **)**  
返回与关联的驱动程序对象**fdo (**<em>x</em>**)**。

可以使用 **！ ks.eval**命令包含这些扩展插件特定的运算符的表达式进行分析，以及[MASM 数字和运算符](masm-numbers-and-operators.md)。

请注意，所有运算符都受 **！ ks.eval** Ks.dll 扩展模块中的所有其他扩展命令也都支持。

下面是举例 **！ ks.eval**正在使用的地址筛选器扩展插件。 请注意在 0x8241C020 地址是否存在[ **！ ks.allstreams** ](-ks-allstreams.md)输出：

```dbgcmd
kd> !eval fdo(829493c4)
Resulting Evaluation: 8241c020

kd> !allstreams
6 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
    Functional Device 8296eb08 [\Driver\wdmaud]
    Functional Device 82490388 [\Driver\sysaudio]
    Functional Device 82970cb8 [\Driver\MSPQM]
    Functional Device 824661b8 [\Driver\MSPCLOCK]
    Functional Device 8241c020 [\Driver\avssamp]
```

 

 





