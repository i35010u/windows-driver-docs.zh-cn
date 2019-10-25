---
title: 突入调试器
description: 突入调试器
ms.assetid: c52c99a2-5db0-49e8-88a7-db075a32c26b
keywords:
- 调试驱动程序 WDK，中断调试器
- 进入调试器 WDK
- 用户模式中断例程 WDK
- 内核模式中断例程 WDK
- 中断例程 WDK
- 条件中断宏 WDK
- 中断宏 WDK
- 例程调试，中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce967354be111c6aa76844c4027375eae676b891
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839580"
---
# <a name="breaking-into-the-debugger"></a>突入调试器


## <span id="ddk_breaking_into_the_debugger_tools"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_TOOLS"></span>


用户模式和内核模式驱动程序使用不同的例程来中断调试器。

### <a name="span-iduser_mode_break_routinesspanspan-iduser_mode_break_routinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>用户模式中断例程

中断例程导致在当前进程中发生异常，以便调用线程可以向与调用进程关联的调试器发出信号。

若要从用户模式程序中断到调试器，请使用**DebugBreak**例程。 其原型如下所示：

```
VOID DebugBreak(VOID);
```

此例程可由包含 windows .h 标头的任何用户模式驱动程序调用。 有关此例程和其他可用于调试的用户模式例程的完整文档，请参阅 Microsoft Windows SDK。

当用户模式程序调用**DebugBreak**时，将发生以下可能的操作：

1.  如果附加了用户模式调试器，程序将中断调试器。 这意味着程序将暂停，调试程序将变为活动状态。

2.  如果未附加用户模式调试器，但在启动时启用了内核模式调试，则整个计算机将进入内核调试器。 如果未连接内核调试器，计算机将冻结并等待内核调试器。

3.  如果未附加用户模式调试器，并且未启用内核模式调试，则程序将终止，并出现未处理的异常，并且将激活事后（实时）调试器。 默认情况下，事后调试程序为 Dr. Watson，这将创建一个故障转储文件，然后询问你是否要将此故障转储文件发送给 Microsoft。

### <a name="span-idkernel_mode_break_routinesspanspan-idkernel_mode_break_routinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>内核模式中断例程

当内核模式程序中断调试器时，整个操作系统会冻结，直到内核调试器允许执行继续执行为止。 如果未提供内核调试器，则将其视为 bug 检查。

[**DbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)例程在内核模式代码中运行，但与**DebugBreak**用户模式例程类似。

[**DbgBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)例程还会导致中断，但它还会将32位状态代码发送到调试器。

当在已检查的生成环境中编译时， [**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))和[**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)例程分别与**DbgBreakPoint**和**DbgBreakPointWithStatus**完全相同。 在免费生成环境中进行编译时，它们不起作用。

### <a name="span-idkernel_mode_conditional_break_macrosspanspan-idkernel_mode_conditional_break_macrosspankernel-mode-conditional-break-macros"></a><span id="kernel_mode_conditional_break_macros"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_MACROS"></span>内核模式条件中断宏

内核模式驱动程序有两个条件中断宏：

-   [**断言**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏测试逻辑表达式。 如果表达式为 false，则执行将停止，并且调试器将变为活动状态。 失败的表达式及其在程序中的位置将显示在调试器中。

-   [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)宏与**ASSERT**完全相同，只是它允许向调试器发送额外的消息。

仅当在已检查的生成环境中编译时， **ASSERT**和**ASSERTMSG**才处于活动状态。 在免费生成环境中进行编译时，它们不起作用。

 

 





