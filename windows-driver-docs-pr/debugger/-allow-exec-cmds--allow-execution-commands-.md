---
title: .allow_exec_cmds（允许执行命令）
description: .Allow_exec_cmds 命令控制是否可以使用执行命令。
keywords:
- .allow_exec_cmds (允许) Windows 调试执行命令
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .allow_exec_cmds (Allow Execution Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2344a84156f39709f0dea6e40be035c3b1d84a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800137"
---
# <a name="allow_exec_cmds-allow-execution-commands"></a>。允许 \_ Exec \_ 命令 (允许执行命令) 


**Allow \_ exec \_** 命令控制是否可以使用执行命令。

```dbgcmd
.allow_exec_cmds 0 
.allow_exec_cmds 1 
.allow_exec_cmds 
```

## <a name="span-idddk_meta_allow_execution_commands_dbgspanspan-idddk_meta_allow_execution_commands_dbgspanparameters"></a><span id="ddk_meta_allow_execution_commands_dbg"></span><span id="DDK_META_ALLOW_EXECUTION_COMMANDS_DBG"></span>参数


<span id="_______0______"></span>**0**   
禁止使用执行命令。

<span id="_______1______"></span>**1**   
允许使用执行命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式和内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关执行命令的完整列表，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果没有参数，则 **. 允许 \_ exec \_** 命令将显示当前是否允许执行命令。

执行命令包括 [**g (中转)**](g--go-.md)， [**t (Trace)**](t--trace-.md)， [**p (步骤)**](p--step-.md)，以及将导致目标执行的任何其他命令或 WinDbg 图形界面操作。

 

 





