---
title: .push（保存调试器状态）
description: .Push 命令保存在调试器的当前状态。
ms.assetid: 2e0b45d6-35b8-4c86-9c54-df8d16b4dcc2
keywords:
- .push （保存调试器状态） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .push (Save Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12e52dd705ed1c0581bad4e3308bd3db336ecdd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335740"
---
# <a name="push-save-debugger-state"></a>.push（保存调试器状态）


**.Push**命令保存在调试器的当前状态。

```dbgcmd
.push
.push /r
.push /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
指定的当前值在伪寄存器**美元 t0**到**美元 t19**应保存。 如果 **/r**不使用参数，这些值不会保存通过 **.push**命令。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
指定安静地执行命令。 也就是说，该命令执行而不显示任何输出。

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

此命令是与一起使用时最有用[脚本](using-script-files.md)并[调试器命令程序](using-debugger-command-programs.md)，以便其可与一个固定的状态。 若要还原到以前保存使用此命令的状态的调试器，请使用[ **.pop （还原调试器状态）** ](-pop--restore-debugger-state-.md)命令。 如果该命令成功，会不显示任何输出。









