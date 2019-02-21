---
title: .fnret （显示函数返回值）
description: .Fnret 命令显示有关函数的返回值的信息。
ms.assetid: b7ce3047-5b0a-43ba-877f-76235139d66c
keywords:
- .fnret （显示函数返回值） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnret (Display Function Return Value)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 51eb7e56fb249b72ba9abf3034e54bad3e17230c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545980"
---
# <a name="fnret-display-function-return-value"></a>.fnret （显示函数返回值）


**.Fnret**命令显示有关函数的返回值的信息。

```dbgcmd
.fnret [/s] Address [Value] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________s______"></span><span id="________S______"></span> **/s**   
集 **$callret**伪寄存器等于正在显示，包括类型信息的返回值。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定函数的地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定要显示的返回值。 如果包括*值*， **.fnret**强制转换*值*到指定的函数的返回类型和返回类型的格式显示它。 如果省略*值*，调试器从返回值寄存器中获取该函数的返回值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果包括*值*参数， **.fnret**命令仅将此值设置为适当的类型强制转换，并显示结果。

如果省略*值*，调试器使用返回值寄存器来确定此值。 如果函数具有比函数的最近返回的*地址*参数指定，将显示的值可能不是此函数返回的值。

 

 





