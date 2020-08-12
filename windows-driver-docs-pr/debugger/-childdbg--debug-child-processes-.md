---
title: .childdbg（调试子进程）
description: Childdbg 命令控制子进程的调试。
ms.assetid: 87d70d3b-d9d5-4a37-b8a7-1616ba78b2f3
keywords:
- childdbg (调试子进程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .childdbg (Debug Child Processes)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 703f331824ff5ce3bb921b04f2a4a7f82c29dc99
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148471"
---
# <a name="childdbg-debug-child-processes"></a>.childdbg（调试子进程）


**Childdbg**命令控制子进程的调试。

```dbgsyntax
.childdbg 0 
.childdbg 1 
.childdbg 
```

## <a name="span-idddk_meta_debug_child_processes_dbgspanspan-idddk_meta_debug_child_processes_dbgspanparameters"></a><span id="ddk_meta_debug_child_processes_dbg"></span><span id="DDK_META_DEBUG_CHILD_PROCESSES_DBG"></span>参数


<span id="_______0______"></span>**0**   
阻止调试器调试子进程。

<span id="_______1______"></span>**1**   
使调试器调试子进程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

只有 Windows XP 和更高版本的 Windows 支持此命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>x86 和 x64</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**子进程**是由原始目标应用程序启动的其他进程。

如果没有参数，则**childdbg**将显示子进程调试的当前状态。

 

 





