---
title: .push（保存调试器状态）
description: Push 命令保存调试器的当前状态。
keywords:
- 。推送 (保存调试器状态) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .push (Save Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a8faaf0a49c20766a75ef0c4ddd035d5b6e160d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821031"
---
# <a name="push-save-debugger-state"></a>.push（保存调试器状态）


**Push** 命令保存调试器的当前状态。

```dbgcmd
.push
.push /r
.push /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________r______"></span><span id="________R______"></span>**/r**   
指定应保存伪寄存器 **$t 0** 到 **$t 19** 之间的当前值。 如果未使用 **/r** 参数，则 **push** 命令不会保存这些值。

<span id="________q______"></span><span id="________Q______"></span>**/q**   
指定命令安静地执行。 也就是说，执行该命令时不显示任何输出。

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

与 [脚本](using-script-files.md) 和 [调试器命令程序](using-debugger-command-programs.md) 一起使用时，此命令最有用，以便能够使用一个固定状态。 若要将调试器还原到以前使用此命令保存的状态，请使用 [**. pop (还原调试器状态)**](-pop--restore-debugger-state-.md) 命令。 如果此命令成功，则不会显示任何输出。









