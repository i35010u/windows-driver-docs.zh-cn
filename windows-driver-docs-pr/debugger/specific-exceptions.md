---
title: 特定异常
description: 特定异常
keywords:
- 特定异常 Windows 调试
topic_type:
- apiref
api_name:
- Specific Exceptions
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc9a3b13ca6d077d83b6c6fe9b4cc1c6e8a30b01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785265"
---
# <a name="specific-exceptions"></a>特定异常


下表列出了特定异常筛选器的异常代码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">异常代码</th>
<th align="left">异常</th>
<th align="left">标头文件或值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_ACCESS_VIOLATION</p></td>
<td align="left"><p>访问冲突</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_ASSERTION_FAILURE</p></td>
<td align="left"><p>断言失败</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_APPLICATION_HANG</p></td>
<td align="left"><p>应用程序挂起</p></td>
<td align="left"><p>0xCFFFFFFF</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_BREAKPOINT</p></td>
<td align="left"><p>中断指令异常</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_CPP_EH_EXCEPTION</p></td>
<td align="left"><p>C + + 异常处理异常</p></td>
<td align="left"><p>0xE06D7363</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_CLR_EXCEPTION</p></td>
<td align="left"><p>公共语言运行时 (CLR) 异常</p></td>
<td align="left"><p>0xE0434f4D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_CONTROL_BREAK</p></td>
<td align="left"><p>CTRL + Break 异常</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_CONTROL_C</p></td>
<td align="left"><p>CTRL + C 例外</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DATATYPE_MISALIGNMENT</p></td>
<td align="left"><p>数据未对齐</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMMAND_EXCEPTION</p></td>
<td align="left"><p>调试器命令异常</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_GUARD_PAGE_VIOLATION</p></td>
<td align="left"><p>保护页冲突</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_ILLEGAL_INSTRUCTION</p></td>
<td align="left"><p>非法指令</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_IN_PAGE_ERROR</p></td>
<td align="left"><p>页内 i/o 错误</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INTEGER_DIVIDE_BY_ZERO</p></td>
<td align="left"><p>整数被零除</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INTEGER_OVERFLOW</p></td>
<td align="left"><p>整数溢出</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_HANDLE</p></td>
<td align="left"><p>句柄无效</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_LOCK_SEQUENCE</p></td>
<td align="left"><p>锁定顺序无效</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_SYSTEM_SERVICE</p></td>
<td align="left"><p>系统调用无效</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_PORT_DISCONNECTED</p></td>
<td align="left"><p>端口断开连接</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_SINGLE_STEP</p></td>
<td align="left"><p>单步例外</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_STACK_BUFFER_OVERRUN</p></td>
<td align="left"><p>堆栈缓冲区溢出</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_STACK_OVERFLOW</p></td>
<td align="left"><p>堆栈溢出</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_VERIFIER_STOP</p></td>
<td align="left"><p>应用程序验证工具停止</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_WAKE_SYSTEM_DEBUGGER</p></td>
<td align="left"><p>唤醒调试器</p></td>
<td align="left"><p>NtStatus。h</p></td>
</tr>
</tbody>
</table>

 

 

 





