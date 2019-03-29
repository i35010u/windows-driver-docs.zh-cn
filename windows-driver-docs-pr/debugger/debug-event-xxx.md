---
title: DEBUG\_EVENT\_XXX
description: 调试\_事件\_XXX 常量是由目标生成的事件标志。
ms.date: 08/13/2018
topic_type:
- apiref
api_name:
- DEBUG_EVENT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 40d0fbc01267f596d8630eb771d13566b5b41b26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566362"
---
# <a name="debugeventxxx"></a>DEBUG\_EVENT\_XXX

目标生成以下事件。

<table>
<tr>
<th>Flag</th>
<th>IDebugEventCallbacksMethod </th>
<th>事件描述</th>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_BREAKPOINT</p>
</td>
<td>
<p><b>IDebugEventCallbacks::Breakpoint</b></p>
</td>
<td>
<p>断点异常出现在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXCEPTION</p>
</td>
<td>
<p><b>IDebugEventCallbacks::Exception</b></p>
</td>
<td>
<p>在目标中发生了异常调试事件。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CREATE_THREAD</p>
</td>
<td>
<p><b>IDebugEventCallbacks::CreateThread</b></p>
</td>
<td>
<p>创建线程调试事件发生在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXIT_THREAD</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ExitThread</b></p>
</td>
<td>
<p>退出线程调试事件出现在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CREATE_PROCESS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::CreateProcess</b></p>
</td>
<td>
<p>创建进程调试事件出现在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXIT_PROCESS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ExitProcess</b></p>
</td>
<td>
<p>退出过程调试事件出现在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_LOAD_MODULE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::LoadModule</b></a></p>
</td>
<td>
<p>模块加载调试事件发生在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_UNLOAD_MODULE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::UnloadModule</b></a></p>
</td>
<td>
<p>模块卸载调试事件发生在目标中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_SYSTEM_ERROR</p>
</td>
<td>
<p><b>IDebugEventCallbacks::SystemError</b></a></p>
</td>
<td>
<p>在目标中发生系统错误。</p>
</td>
</tr>
</table>
<p> </p>
<p>由调试器引擎生成的以下事件。</p>
<table>
<tr>
<th>Flag</th>
<th>IDebugEventCallbacksMethod </th>
<th>描述</th>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_SESSION_STATUS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::SessionStatus</b></p>
</td>
<td>
<p>在会话状态中发生了更改。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_DEBUGGEE_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeDebuggeeState</b></p>
</td>
<td>
<p>引擎已选择或在目标状态中检测到更改。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_ENGINE_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeEngineState</b></a></p>
</td>
<td>
<p>引擎状态已更改。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_SYMBOL_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeSymbolState</b></a></p>
</td>
<td>
<p>符号状态已更改。</p>
</td>
</tr>
</table>

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

 

 





