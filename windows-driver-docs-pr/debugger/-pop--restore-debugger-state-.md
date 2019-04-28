---
title: .pop（还原调试器状态）
description: .Pop 命令将调试程序的状态还原到以前使用.push （保存调试器状态） 命令已保存的状态。
ms.assetid: 31f94b2a-3597-40e4-845a-d686274e36c3
keywords:
- 还原调试器状态 (.pop) 命令
- .pop （还原调试器状态） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pop (Restore Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74d8f2f5878de2a13c3e09e00fcec6e03424b9d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334360"
---
# <a name="pop-restore-debugger-state"></a>.pop（还原调试器状态）


**.Pop**命令将调试程序的状态还原到以前通过使用保存的状态[ **.push （保存调试器状态）** ](-push--save-debugger-state-.md)命令。

```dbgcmd
.pop
.pop /r
.pop /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
指定应还原美元 t0 到 t19 美元的伪寄存器保存的值。 如果 **/r**不是包含，这些值不受 **.pop**命令。

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

此命令是与一起使用时最有用[脚本](using-script-files.md)并[调试器命令程序](using-debugger-command-programs.md)，以便其可与一个固定的状态。 如果该命令成功，会不显示任何输出。

 

 





