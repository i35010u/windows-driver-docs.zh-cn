---
title: 突入调试器
description: 突入调试器
ms.assetid: c52c99a2-5db0-49e8-88a7-db075a32c26b
keywords:
- 调试驱动程序 WDK，中断到调试器
- 中断到调试器 WDK
- 用户模式下中断例程 WDK
- 内核模式下中断例程 WDK
- 中断例程 WDK
- 条件性中断宏 WDK
- 中断宏 WDK
- 调试例程 WDK、 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2eb079e637c2bec5744abd114527c1e7245ac4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344915"
---
# <a name="breaking-into-the-debugger"></a>突入调试器


## <span id="ddk_breaking_into_the_debugger_tools"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_TOOLS"></span>


用户模式和内核模式驱动程序使用不同的例程进入调试器。

### <a name="span-idusermodebreakroutinesspanspan-idusermodebreakroutinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>用户模式下中断例程

中断例程会导致异常发生在当前的过程中，以便调用线程可以指示调试器调用进程与相关联。

若要在用户模式程序从调试器中中断，请使用**DebugBreak**例程。 其原型如下所示：

```
VOID DebugBreak(VOID);
```

此例程可由任何用户模式驱动程序，它包含 windows.h 标头调用。 此例程和其他用户模式下例程用于调试的完整文档，请参阅 Microsoft Windows SDK。

当用户模式程序调用**DebugBreak**，将发生以下可能的操作：

1.  如果用户模式下调试器已附加，程序将进入调试器。 这意味着该程序将暂停，并成为活动部署调试器。

2.  如果用户模式下调试器未附加，但在启动时启用了内核模式调试，整个计算机将进入内核调试器。 如果未附加内核调试程序，计算机将冻结并等待内核调试程序。

3.  如果未附加用户模式下调试程序，且未启用内核模式调试，则程序将终止与未经处理的异常，并将激活的事后 （实时） 调试器。 默认情况下，事后调试器为灾难恢复。Watson，以创建崩溃转储文件然后要求您是否想要向 Microsoft 发送此崩溃转储文件。

### <a name="span-idkernelmodebreakroutinesspanspan-idkernelmodebreakroutinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>内核模式下中断例程

当内核模式程序中断到调试器时，整个操作系统会冻结，直到内核调试程序允许执行继续。 如果内核调试程序不存在，则将此视为 bug 检查。

[ **DbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff543626)例程可在内核模式代码中，但在其他方面类似于**DebugBreak**用户模式下例程。

[ **DbgBreakPointWithStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543629)例程，也会导致中断，但它另外将 32 位的状态代码发送到调试器。

[ **KdBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff548063)并[ **KdBreakPointWithStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff548065)例程相等**DbgBreakPoint**并**DbgBreakPointWithStatus**分别在已检验的版本环境中编译时。 编译时可用的生成环境中，它们会产生任何影响。

### <a name="span-idkernelmodeconditionalbreakmacrosspanspan-idkernelmodeconditionalbreakmacrosspankernel-mode-conditional-break-macros"></a><span id="kernel_mode_conditional_break_macros"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_MACROS"></span>内核模式条件中断宏

两个条件中断宏是适用于内核模式驱动程序：

-   [ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)宏测试的逻辑表达式。 如果表达式为 false，中止程序执行和调试程序将变为活动状态。 在调试器中显示失败的表达式和在程序中的位置。

-   [ **ASSERTMSG** ](https://msdn.microsoft.com/library/windows/hardware/ff542113)宏等同于**ASSERT**相似，只允许发送到调试器的其他消息。

**断言**并**ASSERTMSG**是仅在已检验的版本环境中编译时为活动状态。 编译时可用的生成环境中，它们会产生任何影响。

 

 





