---
title: CTRL+\（调试当前调试器）
description: CTRL + \ 组合键将启动一个新的 CDB 实例;此新调试器使用当前调试器作为其目标。
keywords:
- CTRL + (调试当前调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc554a36ac1537a58c3f5681cf9b1ee7961a158e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783517"
---
# <a name="ctrl-debug-current-debugger"></a>CTRL + \\ (调试当前调试器) 


**CTRL + \\** 键会启动新的 CDB 实例; 此新调试器将使用当前调试器作为其目标。

```dbgcmd
CTRL+\  ENTER 
```

## <span id="ddk_meta_ctrl_p_dbg"></span><span id="DDK_META_CTRL_P_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>调试器</strong></td>
<td align="left"><p>CDB、NTSD、KD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这等效于通过 [**remote.exe**](the-remote-exe-utility.md) 实用工具启动新的 CDB，并使用它来调试已经在运行的调试器。

[**CTRL + \\**](ctrl-alt--.md)类似于 [**. dbgdbg (调试当前调试器)**](-dbgdbg--debug-current-debugger-.md)命令。

 

 





