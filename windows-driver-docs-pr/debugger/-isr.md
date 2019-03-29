---
title: isr
description: Isr 扩展显示指定地址处的 Itanium 中断状态注册 (ISR)。
ms.assetid: 35cf1749-2417-4fd9-9de2-0884ee795ab3
keywords:
- ISR （中断状态注册）
- 中断状态寄存器 (ISR)
- isr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- isr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc29562a30e3b857ee4415a483c13d37a47d62f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565078"
---
# <a name="isr"></a>!isr


！ Isr 扩展显示指定地址处的 Itanium 中断状态注册 (ISR)。

```dbgcmd
!isr Expression [DisplayLevel]
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要显示的 ISR 登记的十六进制地址。 表达式<strong>@isr</strong>还可用于此参数。 在这种情况下，将显示有关当前处理器 ISR 注册的信息。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
显示只有每个 ISR 字段的值。 这是默认设置。

<span id="1"></span>**1**  
显示详细信息的不是保留还是忽略 ISR 字段。

<span id="2"></span>**2**  
显示所有 ISR 字段，包括那些忽略或保留的详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

此扩展命令仅用于 Itanium 目标计算机。

<a name="remarks"></a>备注
-------

下面是输出的几个示例来自此扩展插件：

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

 

 





