---
title: 调试\_状态\_XXX
description: 调试\_状态\_XXX
ms.assetid: 3f5fcdb6-b4fc-4155-bf39-929d00fb210c
ms.date: 12/07/2017
keywords:
- DEBUG_STATUS_XXX Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_STATUS_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 0d519107896a617b3d66091ff2f16a4e447b5434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374837"
---
# <a name="debugstatusxxx"></a>调试\_状态\_XXX


## <span id="ddk_debug_status_xxx_dbx"></span><span id="DDK_DEBUG_STATUS_XXX_DBX"></span>


调试\_状态\_*XXX*状态代码有两个用途。 它们指示引擎如何应继续执行在目标中的，并且它们由引擎报告的执行状态的目标。

事件发生后，引擎可以接收多个说明，以告诉它如何应继续执行在目标中。 在这种情况下，它的作用在指令上具有最高优先级。 通常情况下，较高优先级状态代码表示目标更少执行。

下表中的值是反向按优先顺序; 排序前面表中显示的值具有更高的优先级。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">报告时</th>
<th align="left">指示当</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_NO_DEBUGGEE</p></td>
<td align="left"><p>没有调试会话处于活动状态。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_OUT_OF_SYNC</p></td>
<td align="left"><p>调试器通信通道是同步。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_WAIT_INPUT</p></td>
<td align="left"><p>目标正在等待来自用户的输入。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_TIMEOUT</p></td>
<td align="left"><p>调试器通信通道已超时。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_BREAK</p></td>
<td align="left"><p>挂起目标。</p></td>
<td align="left"><p>挂起目标。</p></td>
<td align="left"><p>最高优先级</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_INTO</p></td>
<td align="left"><p>目标执行一条指令。</p></td>
<td align="left"><p>继续执行的单个指令的目标。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_STEP_BRANCH</p></td>
<td align="left"><p>目标执行到下一步的分支指令。</p></td>
<td align="left"><p>继续执行目标，直至下一个分支指令。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_OVER</p></td>
<td align="left"><p>目标执行单个指令或--如果该指令是子例程调用-子例程。</p></td>
<td align="left"><p>继续执行的单个指令的目标。 如果指令是子例程调用，调用输入和目标可继续运行，直到该子例程返回。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO_NOT_HANDLED</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>继续执行目标，将标记作为未经过处理的事件。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_GO_HANDLED</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>继续执行目标，将事件标记为已处理。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO</p></td>
<td align="left"><p>目标在通常情况下执行。</p></td>
<td align="left"><p>继续正常执行的目标。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_IGNORE_EVENT</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>继续上一次执行目标，忽略该事件。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_RESTART_REQUESTED</p></td>
<td align="left"><p>正在重新启动目标。</p></td>
<td align="left"><p>重新启动目标。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_NO_CHANGE</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>没有指令。 当不希望指示引擎如何继续进行在目标中执行时，由事件回调方法返回此值。</p></td>
<td align="left"><p>最低优先级</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]&gt;状态代码的优先顺序不会遵循常量的数值。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 

 





