---
title: .dbgdbg（调试当前调试器）
description: Dbgdbg 命令启动 CDB 的新实例;此新调试器使用当前调试器作为其目标。
keywords:
- dbgdbg (调试当前调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dbgdbg (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: efb5254599120f78c58609088b1751640f4dd833
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792055"
---
# <a name="dbgdbg-debug-current-debugger"></a>.dbgdbg（调试当前调试器）


**Dbgdbg** 命令启动 CDB 的新实例;此新调试器使用当前调试器作为其目标。

```dbgcmd
.dbgdbg 
```

## <span id="ddk_meta_debug_current_debugger_dbg"></span><span id="DDK_META_DEBUG_CURRENT_DEBUGGER_DBG"></span>


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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Dbgdbg** 命令类似于 [**CTRL + P (调试当前调试器)**](ctrl-p--debug-current-debugger-.md)控制键。 不过， **dbgdbg** 更通用，因为它可以从 WINDBG 以及 KD 和 CDB 中使用，并且可用于调试远程计算机上的调试服务器。

 

 





