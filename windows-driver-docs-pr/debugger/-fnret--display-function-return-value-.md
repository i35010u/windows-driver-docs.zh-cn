---
title: .fnret（显示函数返回值）
description: Fnret 命令显示有关函数的返回值的信息。
keywords:
- fnret (显示) Windows 调试的函数返回值
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnret (Display Function Return Value)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2418ea80da0bd665f1d7c040db10bab058a2d66a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815523"
---
# <a name="fnret-display-function-return-value"></a>.fnret（显示函数返回值）


**Fnret** 命令显示有关函数的返回值的信息。

```dbgcmd
.fnret [/s] Address [Value] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________s______"></span><span id="________S______"></span>**/s**   
将 **$callret** 伪寄存器设置为等于正在显示的返回值，包括类型信息。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定函数的地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定要显示的返回值。 如果包含 *值*，则 **fnret** 将 *值* 强制转换为指定函数的返回类型，并以返回类型的格式显示。 如果省略 *值*，调试器将从返回值寄存器中获取函数的返回值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果包含 *value* 参数，则 **fnret** 命令只会将此值转换为正确的类型并显示结果。

如果省略 *值*，调试器将使用返回值寄存器来确定此值。 如果函数返回的值晚于 *Address* 参数指定的函数，则显示的值可能不是此函数返回的值。

 

 





