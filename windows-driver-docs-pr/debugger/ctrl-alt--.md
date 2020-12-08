---
title: 'CTRL + ALT + \ (调试当前调试器) '
description: CTRL + ALT + \ 组合键将启动一个新的 CDB 实例;此新调试器使用当前调试器作为其目标。
keywords:
- CTRL + ALT + (调试当前调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+ALT+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d2591751902e4ebe77103a627531a5f7c8cce7ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839029"
---
# <a name="ctrlalt-debug-current-debugger"></a>CTRL + ALT + \\ (调试当前调试器) 


**CTRL + ALT + \\** 键会启动新的 CDB 实例; 此新调试器将使用当前调试器作为其目标。

```dbgcmd
CTRL+ALT+\ 
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
<td align="left"><p>WinDbg</p></td>
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

**CTRL + ALT + \\** 类似于 [**. dbgdbg (调试当前调试器)**](-dbgdbg--debug-current-debugger-.md)命令，但 **CTRL + ALT + \\** 具有可在没有调试器命令行可用时使用的优点。

 

 





