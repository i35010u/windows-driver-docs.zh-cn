---
title: psp
description: Psp 扩展显示 (PSP) 在指定地址注册的处理器状态参数。
keywords:
- '处理器状态参数 (PSP) '
- PSP 寄存器
- psp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- psp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 659937c4b08ea3bdf4dc735685efe7033d189016
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821055"
---
# <a name="psp"></a>!psp


**！ Psp** 扩展显示 (psp) 在指定地址注册的处理器状态参数。

此扩展仅在基于 Itanium 的目标计算机上受支持。

```dbgcmd
!psp Address [DisplayLevel]
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 PSP 寄存器的十六进制地址。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
仅显示每个 PSP 字段的值。 这是默认值。

<span id="1"></span>**1**  
显示有关每个不是保留或忽略的 PSP 字段的详细信息。

<span id="2"></span>**pps-2**  
显示有关所有 PSP 字段的更深入信息，包括那些被忽略或保留的字段。

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

 

 

 





