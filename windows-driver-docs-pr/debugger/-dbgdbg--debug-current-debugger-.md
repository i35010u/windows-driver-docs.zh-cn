---
title: .dbgdbg（调试当前调试器）
description: .Dbgdbg 命令启动 CDB; 的新实例此新调试器将当前的调试器作为其目标。
ms.assetid: a90392b5-d8ae-495d-8074-060e4ec89037
keywords:
- .dbgdbg （调试当前调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dbgdbg (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20c74ab6390a7a18b07aee3df31d3456691ab24d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336888"
---
# <a name="dbgdbg-debug-current-debugger"></a>.dbgdbg（调试当前调试器）


**.Dbgdbg**命令启动 CDB 的新实例; 此新调试器所需的当前调试器作为其目标。

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

**.Dbgdbg**命令是类似于[ **CTRL + P （调试当前调试器）** ](ctrl-p--debug-current-debugger-.md)控制密钥。 但是， **.dbgdbg**是更灵活，因为可以从 WinDbg、 KD 和 CDB，使用它，并且可用于调试在远程计算机上的调试服务器。

 

 





