---
title: isr
description: Isr 扩展显示指定地址 (ISR) 的 Itanium 中断状态寄存器。
keywords:
- 'ISR (中断状态注册) '
- " (ISR) 中断状态注册"
- isr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- isr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 581de1089b61e9ae6c46f0ec9977182d4be98157
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786491"
---
# <a name="isr"></a>!isr


！ Isr 扩展显示指定地址 (ISR) 的 Itanium 中断状态寄存器。

```dbgcmd
!isr Expression [DisplayLevel]
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要显示的 ISR 寄存器的十六进制地址。 表达式 <strong>@isr</strong> 还可用于此参数。 在这种情况下，将显示有关当前处理器 ISR 注册的信息。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
仅显示每个 ISR 字段的值。 这是默认值。

<span id="1"></span>**1**  
显示有关非保留或忽略的 ISR 字段的详细信息。

<span id="2"></span>**pps-2**  
显示有关所有 ISR 字段的详细信息，包括已忽略或保留的字段。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令只能与 Itanium 目标计算机一起使用。

<a name="remarks"></a>备注
-------

下面是此扩展的几个输出示例：

```dbgcmd
kd> !isr @isr
isr:ed ei so ni ir rs sp na r w x vector code
  0  0  0  0  0  0  0  0 0 0 0      0   0

kd> !isr @isr 2

 cod : 0 : interruption Code
 vec : 0 : IA32 exception vector number
  rv : 0 : reserved0
   x : 0 : eXecute exception
   w : 0 : Write exception
   r : 0 : Read exception
  na : 0 : Non-Access exception
  sp : 0 : Speculative load exception
  rs : 0 : Register Stack
  ir : 0 : Invalid Register frame
  ni : 0 : Nested Interruption
  so : 0 : IA32 Supervisor Override
  ei : 0 : Exception IA64 Instruction
  ed : 0 : Exception Deferral
  rv : 0 : reserved1
```

 

 





