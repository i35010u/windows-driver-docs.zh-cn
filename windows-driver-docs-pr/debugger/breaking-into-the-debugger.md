---
title: 突入调试器
description: 突入调试器
ms.assetid: 4fec7170-7480-4a8a-b060-1c8a8c3fb9dc
keywords:
- 中断到调试器
- DebugBreak 函数
- DbgBreakPoint 函数
- KdBreakPoint 函数
- DbgBreakPointWithStatus 函数
- KdBreakPointWithStatus 函数
- ASSERT 宏
- ASSERTMSG 宏
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbeeec83d71201a4c58be5d507477d2c72b32b45
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209093"
---
# <a name="breaking-into-the-debugger"></a>突入调试器


## <span id="ddk_breaking_into_the_debugger_dbg"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_DBG"></span>

用户模式和内核模式代码使用不同的例程来中断调试器。

### <a name="span-iduser_mode_break_routinesspanspan-iduser_mode_break_routinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>用户模式中断例程

中断例程导致在当前进程中发生异常，以便调用线程可以向与调用进程关联的调试器发出信号。

若要从用户模式程序中断到调试器，请使用[DebugBreak 函数](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)。 

当用户模式程序调用**DebugBreak**时，将发生以下可能的操作：

1.  如果附加了用户模式调试器，程序将中断调试器。 这意味着程序将暂停，调试程序将变为活动状态。

2.  如果未附加用户模式调试器，但在启动时启用了内核模式调试，则整个计算机将进入内核调试器。 如果未连接内核调试器，计算机将冻结并等待内核调试器。

3.  如果没有附加用户模式调试器，并且未启用内核模式调试，则程序将终止，并出现未经处理的异常，并将激活事后（实时）调试程序。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

### <a name="span-idkernel_mode_break_routinesspanspan-idkernel_mode_break_routinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>内核模式中断例程

当内核模式程序中断调试器时，整个操作系统会冻结，直到内核调试器允许执行继续执行为止。 如果没有内核调试器，则将其视为 bug 检查。

**DbgBreakPoint**例程在内核模式代码中运行，但与**DebugBreak**用户模式例程类似。

**DbgBreakPointWithStatus**也会导致中断，但它还会将32位状态代码发送到调试器。

在已检查的生成环境中编译时， **KdBreakPoint**和**KdBreakPointWithStatus**分别与**DbgBreakPoint**和**DbgBreakPointWithStatus**相同。 在免费生成环境中进行编译时，它们不起作用。

### <a name="span-idkernel_mode_conditional_break_routinesspanspan-idkernel_mode_conditional_break_routinesspankernel-mode-conditional-break-routines"></a><span id="kernel_mode_conditional_break_routines"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_ROUTINES"></span>内核模式条件中断例程

内核模式代码有两个条件中断例程。 这些例程测试逻辑表达式。 如果表达式为 false，则执行将停止，并且调试器将变为活动状态。

**ASSERT**宏使调试器显示失败的表达式及其在程序中的位置。 **ASSERTMSG**宏类似，但允许向调试器发送额外的消息。

仅当在已检查的生成环境中编译时， **ASSERT**和**ASSERTMSG**才处于活动状态。 在免费生成环境中进行编译时，它们不起作用。

有关这些例程以及生成环境的完整文档，请参阅 Windows 驱动程序工具包。

 

 





