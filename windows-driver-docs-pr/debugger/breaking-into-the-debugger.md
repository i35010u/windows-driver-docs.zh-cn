---
title: 突入调试器
description: 突入调试器
keywords:
- 中断到调试器
- DebugBreak 函数
- DbgBreakPoint 函数
- KdBreakPoint 函数
- DbgBreakPointWithStatus 函数
- KdBreakPointWithStatus 函数
- ASSERT 宏
- ASSERTMSG 宏
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: a50ac21a9183158702f2b95ed25adcceecd4cfb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788897"
---
# <a name="breaking-into-the-debugger"></a>突入调试器

用户模式和内核模式代码使用不同的例程来中断调试器。

## <a name="user-mode-break-routines"></a>User-Mode 中断例程

中断例程导致在当前进程中发生异常，以便调用线程可以向与调用进程关联的调试器发出信号。

若要从用户模式程序中断到调试器，请使用 [DebugBreak 函数](/windows/win32/api/debugapi/nf-debugapi-debugbreak)。 其原型如下所示：

```cpp
VOID DebugBreak(VOID);
```

当用户模式程序调用 **DebugBreak** 时，将发生以下可能的操作：

1. 如果附加了用户模式调试器，程序将中断调试器。 这意味着程序将暂停，调试程序将变为活动状态。

2. 如果未附加用户模式调试器，但在启动时启用了内核模式调试，则整个计算机将进入内核调试器。 如果未连接内核调试器，计算机将冻结并等待内核调试器。

3. 如果未附加用户模式调试器，并且未启用内核模式调试，则程序将终止，并出现未处理的异常，并且将激活事后 (实时) 调试器。 有关详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。

## <a name="kernel-mode-break-routines"></a>Kernel-Mode 中断例程

当内核模式程序中断调试器时，整个操作系统会冻结，直到内核调试器允许执行继续执行为止。 如果没有内核调试器，则将其视为 bug 检查。

[**DbgBreakPoint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)例程在内核模式代码中运行，但与 **DebugBreak** 用户模式例程类似。

[**DbgBreakPointWithStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)例程还会导致中断，但它还会将32位状态代码发送到调试器。

当在已检查的生成环境中编译时， [**KdBreakPoint**](/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85)) 和 [**KdBreakPointWithStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus) 例程分别与 **DbgBreakPoint** 和 **DbgBreakPointWithStatus** 完全相同。 在免费生成环境中进行编译时，它们不起作用。

## <a name="kernel-mode-conditional-break-routines"></a>Kernel-Mode 条件中断例程

内核模式代码有两个条件中断例程。 这些例程测试逻辑表达式。 如果表达式为 false，则执行将停止，并且调试器将变为活动状态。

- [**断言**](/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏测试逻辑表达式。 如果表达式为 false，则执行将停止，并且调试器将变为活动状态。 失败的表达式及其在程序中的位置将显示在调试器中。

- [**ASSERTMSG**](/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)宏与 **ASSERT** 完全相同，只是它允许向调试器发送额外的消息。

仅当在已检查的生成环境中编译时， **ASSERT** 和 **ASSERTMSG** 才处于活动状态。 在免费生成环境中进行编译时，它们不起作用。
