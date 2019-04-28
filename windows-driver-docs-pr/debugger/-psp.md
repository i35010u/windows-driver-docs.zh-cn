---
title: psp
description: Psp 扩展显示指定地址处的处理器状态参数 (PSP) 注册。
ms.assetid: 5ed36051-31e0-405f-ac30-88d888f9d915
keywords:
- 处理器状态参数 (PSP)
- PSP 注册
- psp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- psp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5214b39c5db25f64ae38ea49d2fb10dfeaac52db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334332"
---
# <a name="psp"></a>!psp


**！ Psp**扩展指定地址处显示处理器状态参数 (PSP) 注册。

仅在基于 Itanium 的目标计算机上支持此扩展。

```dbgcmd
!psp Address [DisplayLevel]
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的 PSP 登记的十六进制地址。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
可以是下列选项之一：

<span id="0"></span>**0**  
显示只有 PSP 的每个字段的值。 这是默认设置。

<span id="1"></span>**1**  
显示有关每个不保留或忽略的 PSP 字段更深入的信息。

<span id="2"></span>**2**  
显示上的所有 PSP 字段，包括那些忽略或保留更深入的信息。

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

 

 

 





