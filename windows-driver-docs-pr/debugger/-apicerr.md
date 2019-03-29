---
title: apicerr
description: Apicerr 扩展显示本地高级可编程中断控制器 (APIC) 错误日志。
ms.assetid: b058412b-a4df-42cc-8550-b5db4e0bbccc
keywords:
- APIC （高级可编程中断控制器）
- apicerr Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- apicerr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44c6a1f059f87ec4f4c64993ff2831b38d71f0b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564954"
---
# <a name="apicerr"></a>!apicerr


**！ Apicerr**扩展显示本地高级可编程中断控制器 (APIC) 错误日志。

```dbgcmd
     !apicerr [Format] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Format______"></span><span id="_______format______"></span><span id="_______FORMAT______"></span> *格式*   
指定要在其中显示错误日志内容的顺序。 这可以是以下值之一：

<span id="0x0"></span><span id="0X0"></span>0x0  
显示的匹配项的顺序比较的错误日志。

<span id="0x1"></span><span id="0X1"></span>0x1  
显示根据处理器的错误日志。

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

 

此扩展命令仅可用于基于 x86 或基于 x64 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Apic 有关的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这本书不可能在某些语言和国家/地区中可用。）

 

 





