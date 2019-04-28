---
title: .childdbg（调试子进程）
description: .Childdbg 命令控制子进程调试。
ms.assetid: 87d70d3b-d9d5-4a37-b8a7-1616ba78b2f3
keywords:
- .childdbg （调试子进程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .childdbg (Debug Child Processes)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83df9291f16ec69bc8a1286e5d098fc77352e44b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334632"
---
# <a name="childdbg-debug-child-processes"></a>.childdbg（调试子进程）


**.Childdbg**命令控制子进程调试。

```dbgsyntax
.childdbg 0 
.childdbg 1 
.childdbg 
```

## <a name="span-idddkmetadebugchildprocessesdbgspanspan-idddkmetadebugchildprocessesdbgspanparameters"></a><span id="ddk_meta_debug_child_processes_dbg"></span><span id="DDK_META_DEBUG_CHILD_PROCESSES_DBG"></span>参数


<span id="_______0______"></span> **0**   
使调试器无法调试子进程。

<span id="_______1______"></span> **1**   
使调试器来调试子进程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅支持 Windows XP 和更高版本的 Windows 中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>x86、 x64 和 Itanium 仅</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**子进程**是由原始目标应用程序启动的其他进程。

不带任何参数， **.childdbg**将显示的子进程调试的当前状态。

 

 





