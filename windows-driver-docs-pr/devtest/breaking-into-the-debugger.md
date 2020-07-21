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
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 583e7206e3e5a7c1ef25942ac26947c69031e162
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86568066"
---
# <a name="breaking-into-the-debugger"></a>突入调试器

用户模式和内核模式驱动程序使用不同的例程来中断调试器。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

## <a name="user-mode-break-routines"></a>用户模式中断例程

中断例程导致在当前进程中发生异常，以便调用线程可以向与调用进程关联的调试器发出信号。

若要从用户模式程序中断到调试器，请使用**DebugBreak**例程。 其原型如下所示：

```cpp
VOID DebugBreak(VOID);
```

此例程可由包含 windows .h 标头的任何用户模式驱动程序调用。 有关此例程和其他可用于调试的用户模式例程的完整文档，请参阅 Microsoft Windows SDK。

当用户模式程序调用**DebugBreak**时，将发生以下可能的操作：

1. 如果附加了用户模式调试器，程序将中断调试器。 这意味着程序将暂停，调试程序将变为活动状态。

1. 如果未附加用户模式调试器，但在启动时启用了内核模式调试，则整个计算机将进入内核调试器。 如果未连接内核调试器，计算机将冻结并等待内核调试器。

1. 如果未附加用户模式调试器，并且未启用内核模式调试，则程序将终止，并出现未处理的异常，并且将激活事后（实时）调试器。 默认情况下，事后调试程序为 Dr. Watson，这将创建一个故障转储文件，然后询问你是否要将此故障转储文件发送给 Microsoft。

## <a name="kernel-mode-break-routines"></a>内核模式中断例程

当内核模式程序中断调试器时，整个操作系统会冻结，直到内核调试器允许执行继续执行为止。 如果未提供内核调试器，则将其视为 bug 检查。

[**DbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)例程在内核模式代码中运行，但与**DebugBreak**用户模式例程类似。

[**DbgBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)例程还会导致中断，但它还会将32位状态代码发送到调试器。

当在已检查的生成环境中编译时， [**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))和[**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)例程分别与**DbgBreakPoint**和**DbgBreakPointWithStatus**完全相同。 在免费生成环境中进行编译时，它们不起作用。

## <a name="kernel-mode-conditional-break-macros"></a>内核模式条件中断宏

内核模式驱动程序有两个条件中断宏：

- [**断言**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏测试逻辑表达式。 如果表达式为 false，则执行将停止，并且调试器将变为活动状态。 失败的表达式及其在程序中的位置将显示在调试器中。

- [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)宏与**ASSERT**完全相同，只是它允许向调试器发送额外的消息。

仅当在已检查的生成环境中编译时， **ASSERT**和**ASSERTMSG**才处于活动状态。 在免费生成环境中进行编译时，它们不起作用。
