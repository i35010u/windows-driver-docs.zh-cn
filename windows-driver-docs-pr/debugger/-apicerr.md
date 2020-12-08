---
title: apicerr
description: Apicerr 扩展显示 (APIC) 错误日志的本地高级可编程中断控制器。
keywords:
- 'APIC (高级可编程中断控制器) '
- apicerr Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- apicerr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12de059c4a66639e99334ba190852e7247f32f9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800035"
---
# <a name="apicerr"></a>!apicerr


**！ Apicerr** 扩展显示 (APIC) 错误日志的本地高级可编程中断控制器。

```dbgcmd
     !apicerr [Format] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Format______"></span><span id="_______format______"></span><span id="_______FORMAT______"></span>*格式*   
指定错误日志内容的显示顺序。 这可以是以下值之一：

<span id="0x0"></span><span id="0X0"></span>0x0  
根据出现顺序显示错误日志。

<span id="0x1"></span><span id="0X1"></span>0x1  
根据处理器显示错误日志。

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

 

此扩展命令只能与基于 x86 或基于 x64 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 APICs 的信息，请参阅 Russinovich 和 David 的 *Microsoft Windows 内部机制* 。 

 

 





