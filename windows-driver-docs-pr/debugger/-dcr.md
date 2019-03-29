---
title: dcr
description: Dcr 扩展显示指定地址处的默认控制寄存器 (DCR)。
ms.assetid: 294fc3a9-5182-47ae-a261-53be6389bcf1
keywords:
- DCR （默认值控制寄存器）
- dcr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80e3f305d137335cb84401f75007acade430656e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565095"
---
# <a name="dcr"></a>!dcr


**！ Dcr**扩展指定地址处显示的默认控制寄存器 (DCR)。

```dbgcmd
!dcr Expression [DisplayLevel]
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定 DCR 要显示的十六进制地址。 表达式<strong>@dcr</strong>还可用于此参数。 在这种情况下，将显示有关当前处理器 DCR 信息。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
将导致仅显示每个 DCR 字段的值。 这是默认值。

<span id="1"></span>**1**  
将导致显示以包括有关每个 DCR 字段不是保留或忽略的进一步信息。

<span id="2"></span>**2**  
将导致显示以包括有关所有 DCR 字段，包括那些忽略或保留的进一步信息。

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

 

此扩展命令仅用于基于 Itanium 的目标计算机。

<a name="remarks"></a>备注
-------

DCR 指定处理器状态的默认参数注册上中断的值。 DCR 还指定了一些附加的全局控件，以及可以推迟推理负载错误。

下面是几个示例：

```dbgcmd
kd> !dcr @dcr
dcr:pp be lc dm dp dk dx dr da dd
1 0 1 1 1 1 1 1 1 1

kd> !dcr @dcr 2

  pp : 1 : Privileged Performance Monitor Default
  be : 0 : Big-Endian Default
  lc : 1 : IA-32 Lock check Enable
  rv : 0 : reserved1
  dm : 1 : Defer TLB Miss faults only
  dp : 1 : Defer Page Not Present faults only
  dk : 1 : Defer Key Miss faults only
  dx : 1 : Defer Key Permission faults only
  dr : 1 : Defer Access Rights faults only
  da : 1 : Defer Access Bit faults only
  dd : 0 : Defer Debug faults only
  rv : 0 : reserved2
```

 

 





