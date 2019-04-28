---
title: pmc
description: Pmc 扩展显示指定地址处的性能监视器计数器 (PMC) 注册。
ms.assetid: ff9a03af-f0e9-4aef-b583-c3092eb5f89c
keywords:
- 性能监视器计数器 (PMC)
- pmc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pmc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2145f09a4554d72e778d79fa9e31a0ff10959ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334383"
---
# <a name="pmc"></a>!pmc


**！ Pmc**扩展指定地址处显示的性能监视器计数器 (PMC) 寄存器。

只能在基于 Itanium 的目标计算机上支持此扩展。

```dbgcmd
!pmc [- Option] Expression [DisplayLevel]
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *选项*   
可以是以下值之一：

<span id="gen"></span><span id="GEN"></span>**gen**  
显示为泛型的 PMC 注册的注册。

<span id="btb"></span><span id="BTB"></span>**btb**  
显示注册为分支跟踪缓冲区 (BTB) PMC 寄存器。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定 PMC 的十六进制地址。 表达式<strong>@kpfcgen</strong>并<strong>@kpfcbtb</strong>可以用作此参数的值。

如果*表达式*是<strong>@kpfcgen</strong>，调试器将显示当前处理器 PMC 注册为泛型 PMC 寄存器。 您还可以显示当前处理器 PMC 通过设置注册为泛型 PMC 寄存器*选项*到**常规**并使用<strong>@kpfc4</strong>，  <strong>@kpfc5</strong>， <strong>@kpfc6</strong>，或<strong>@kpfc7</strong>对于*表达式*值。

如果*表达式*是<strong>@kpfcbtb</strong>，调试器将显示当前处理器 PMC 注册为 BTB PMC 注册。 您还可以显示当前处理器 PMC 通过设置注册为 BTB PMC 寄存器*选项*到**btb**并使用@kpfc12有关*表达式*值。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
可以是以下值之一：

<span id="0"></span>**0**  
显示每个 PMC 值寄存器字段。 这是默认设置。

<span id="1"></span>**1**  
有关 PMC 的显示详细的信息注册不是保留还是忽略的字段。

<span id="2"></span>**2**  
显示有关所有 PMC 的详细的信息注册字段，包括那些忽略或保留。

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

 

 

 





