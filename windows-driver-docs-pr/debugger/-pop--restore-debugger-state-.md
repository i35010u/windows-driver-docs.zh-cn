---
title: .pop（还原调试器状态）
description: Pop 命令将调试器状态还原到以前使用 "推送 (保存调试器状态") 命令保存的状态。
keywords:
- " ( 中还原调试器状态。) 命令"
- 。 pop (还原调试器状态) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pop (Restore Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1c48fc133b2eb26718819c54f39962dbc961609b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791701"
---
# <a name="pop-restore-debugger-state"></a>.pop（还原调试器状态）


**Pop** 命令将调试器状态还原到以前使用 "[**推送 (保存调试器状态")**](-push--save-debugger-state-.md)命令保存的状态。

```dbgcmd
.pop
.pop /r
.pop /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________r______"></span><span id="________R______"></span>**/r**   
指定应还原伪寄存器 $t 0 到 $t 19 的已保存值。 如果不包含 **/r** ，则这些值不受 **. pop** 命令的影响。

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

与 [脚本](using-script-files.md) 和 [调试器命令程序](using-debugger-command-programs.md) 一起使用时，此命令最有用，以便能够使用一个固定状态。 如果此命令成功，则不会显示任何输出。

 

 





