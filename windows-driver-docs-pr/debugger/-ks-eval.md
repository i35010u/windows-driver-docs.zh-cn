---
title: ks. eval
description: Ks extension 使用扩展特定的表达式计算器来计算表达式的值。
keywords:
- ks eval Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.eval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b61d864c4cda5ce3c9333fd2396c71f2dfcaa2d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828297"
---
# <a name="kseval"></a>!ks.eval


**！ Ks** extension 使用扩展特定的表达式计算器来计算表达式的值。

```dbgcmd
!ks.eval Expression 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要计算的表达式。 *表达式* 可以包含任何 MASM 运算符、符号或数字语法，还可以包含下面描述的扩展特定的运算符。 有关 MASM 表达式的详细信息，请参阅 [Masm 数字和运算符](masm-numbers-and-operators.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

扩展模块包括两个特定于扩展的运算符，可用于扩展命令的 address 参数：

<span id="________fdo_________x_________"></span><span id="________FDO_________X_________"></span>**fdo (** *x* **)**  
返回与地址 **x** 上的对象关联的功能设备对象。

<span id="________driver_________x_________"></span><span id="________DRIVER_________X_________"></span>**驱动程序 (** *x* **)**  
返回与 **fdo (** <em>x</em> **)** 相关联的驱动程序对象。

您可以使用 **！ ks. eval** 命令分析包含这些特定于扩展的运算符以及 [MASM 数字和运算符](masm-numbers-and-operators.md)的表达式。

请注意，Ks.dll 扩展模块中的所有其他扩展命令也支持 **！ ks** 所支持的所有运算符。

下面是用于筛选器地址的 **！ ks. eval** 扩展的一个示例。 请注意，0x8241C020 地址存在于 [**！ allstreams**](-ks-allstreams.md) 输出中：

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

 

 





