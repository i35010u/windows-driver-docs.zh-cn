---
title: pmc
description: Pmc 扩展显示 (PMC) 在指定地址注册的性能监视器计数器。
keywords:
- '性能监视器计数器 (PMC) '
- pmc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pmc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75f73cc8c0269fe971868ec28da88bed1b0ad161
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817017"
---
# <a name="pmc"></a>!pmc


**！ Pmc** 扩展显示 (pmc) 在指定地址注册的性能监视器计数器。

此扩展仅在基于 Itanium 的目标计算机上受支持。

```dbgcmd
!pmc [- Option] Expression [DisplayLevel]
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项*   
可以是以下值之一：

<span id="gen"></span><span id="GEN"></span>**常规**  
显示 register 作为一般 PMC 注册。

<span id="btb"></span><span id="BTB"></span>**btb**  
显示 register 作为分支跟踪缓冲区 (BTB) PMC register。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定 PMC 的十六进制地址。 表达式 <strong>@kpfcgen</strong> 和 <strong>@kpfcbtb</strong> 可用作此参数的值。

如果 *Expression* 为 <strong>@kpfcgen</strong> ，则调试器会显示当前处理器 PMC REGISTER 作为一般 PMC 寄存器。 还可以通过将 *选项* 设置为 "生成" **，并对** <strong>@kpfc4</strong> <strong>@kpfc5</strong> <strong>@kpfc6</strong> <strong>@kpfc7</strong> *表达式* 值使用、、或，将当前处理器 PMC 注册显示为通用 PMC 寄存器。

如果 *Expression* 为 <strong>@kpfcbtb</strong> ，则调试器会将当前处理器 PMC REGISTER 显示为 BTB PMC register。 还可以通过将 *选项* 设置为 **BTB** ，并使用 @kpfc12 作为 *表达式* 值，来显示当前处理器 PMC register 作为 BTB PMC register。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
可以是以下值之一：

<span id="0"></span>**0**  
仅显示每个 PMC 注册字段的值。 这是默认值。

<span id="1"></span>**1**  
显示有关非保留或忽略的 PMC 寄存器字段的详细信息。

<span id="2"></span>**pps-2**  
显示有关所有 PMC 注册字段的详细信息，包括已忽略或保留的字段。

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

 

 

 





