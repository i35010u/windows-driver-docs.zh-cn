---
title: .allow_exec_cmds （允许执行命令）
description: .Allow_exec_cmds 命令控制是否可以使用执行命令。
ms.assetid: c6e37cf1-42cc-4f82-9eb8-d252f0b6e196
keywords:
- .allow_exec_cmds （允许执行命令） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .allow_exec_cmds (Allow Execution Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b81c201ee4429b131c1e7f41f00814cae541f724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544219"
---
# <a name="allowexeccmds-allow-execution-commands"></a>.allow\_exec\_传送的命令 （允许执行命令）


**.Allow\_exec\_传送的命令**命令控件是否可以使用执行命令。

```dbgcmd
.allow_exec_cmds 0 
.allow_exec_cmds 1 
.allow_exec_cmds 
```

## <a name="span-idddkmetaallowexecutioncommandsdbgspanspan-idddkmetaallowexecutioncommandsdbgspanparameters"></a><span id="ddk_meta_allow_execution_commands_dbg"></span><span id="DDK_META_ALLOW_EXECUTION_COMMANDS_DBG"></span>参数


<span id="_______0______"></span> **0**   
禁止使用执行命令。

<span id="_______1______"></span> **1**   
允许使用执行命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式和内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

执行命令的完整列表，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

不带任何参数， **.allow\_exec\_传送的命令**是否当前允许执行命令将显示。

执行命令，包括[ **g （转向）**](g--go-.md)， [ **t (Trace)**](t--trace-.md)， [ **p （步骤）** ](p--step-.md)，和任何其他命令或 WinDbg 图形界面操作会导致要执行的目标。

 

 





