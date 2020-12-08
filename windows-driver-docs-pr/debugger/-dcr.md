---
title: dcr
description: Dcr 扩展显示 (DCR) 指定地址处的默认控制寄存器。
keywords:
- 'DCR (默认控制寄存器) '
- dcr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a38b2616693aa9a726c5aab93d662dba381672d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798461"
---
# <a name="dcr"></a>!dcr


**！ Dcr** extension 显示指定地址 (dcr) 的默认控制寄存器。

```dbgcmd
!dcr Expression [DisplayLevel]
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要显示的 DCR 的十六进制地址。 表达式 <strong>@dcr</strong> 还可用于此参数。 在这种情况下，将显示有关当前处理器 DCR 的信息。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
导致只显示每个 DCR 字段的值。 这是默认值。

<span id="1"></span>**1**  
使显示内容包括有关每个不是保留或忽略的 DCR 字段的更深入信息。

<span id="2"></span>**pps-2**  
使显示内容包含有关所有 DCR 字段的更深入信息，包括那些已忽略或保留的字段。

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

 

此扩展命令只能与基于 Itanium 的目标计算机一起使用。

<a name="remarks"></a>备注
-------

DCR 为中断时的处理器状态寄存器值指定默认参数。 DCR 还指定了一些其他全局控件，以及是否可以延迟推理加载错误。

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

 

 





