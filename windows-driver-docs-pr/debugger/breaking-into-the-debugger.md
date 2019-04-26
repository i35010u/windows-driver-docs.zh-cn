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
ms.openlocfilehash: f10e442ea7c18f65d4ddd8330555777618dcbe0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327355"
---
# <a name="breaking-into-the-debugger"></a>突入调试器


## <span id="ddk_breaking_into_the_debugger_dbg"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_DBG"></span>

用户模式和内核模式代码使用不同的例程来中断调试器。

### <a name="span-idusermodebreakroutinesspanspan-idusermodebreakroutinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>用户模式下中断例程

中断例程会导致异常发生在当前的过程中，以便调用线程可以指示调试器调用进程与相关联。

若要在用户模式程序从调试器中中断，请使用[DebugBreak 函数](https://msdn.microsoft.com/library/windows/desktop/ms679297(v=vs.85).aspx)。 

当用户模式程序调用**DebugBreak**，将发生以下可能的操作：

1.  如果用户模式下调试器已附加，程序将进入调试器。 这意味着该程序将暂停，并成为活动部署调试器。

2.  如果没有任何用户模式下调试程序附加，但在启动时启用了内核模式调试，整个计算机将进入内核调试器。 如果没有内核调试器已附加，计算机将冻结并等待内核调试程序。

3.  如果没有任何用户模式下调试程序附加，并且未启用内核模式调试，则程序将终止与未经处理的异常，并将激活的事后 （实时） 调试器。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

### <a name="span-idkernelmodebreakroutinesspanspan-idkernelmodebreakroutinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>内核模式下中断例程

当内核模式程序中断到调试器时，整个操作系统会冻结，直到内核调试程序允许执行继续。 如果没有内核调试程序存在，则将此视为 bug 检查。

**DbgBreakPoint**例程可在内核模式代码中，但在其他方面类似于**DebugBreak**用户模式下例程。

**DbgBreakPointWithStatus**还会导致中断，但它另外 32 位的状态将代码发送到调试器。

**KdBreakPoint**和**KdBreakPointWithStatus**等于**DbgBreakPoint**并**DbgBreakPointWithStatus**分别在编译时已检验的版本环境。 编译时可用的生成环境中，它们会产生任何影响。

这些例程，以及生成环境的完整文档，请参阅 Windows 驱动程序工具包。

### <a name="span-idkernelmodeconditionalbreakroutinesspanspan-idkernelmodeconditionalbreakroutinesspankernel-mode-conditional-break-routines"></a><span id="kernel_mode_conditional_break_routines"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_ROUTINES"></span>内核模式条件中断例程

两个条件中断例程是适用于内核模式代码。 这些例程测试的逻辑表达式。 如果表达式为 false，中止程序执行和调试程序将变为活动状态。

**ASSERT**宏会导致调试器在程序中显示失败的表达式和其位置。 **ASSERTMSG**宏非常相似，但是允许的其他消息发送到调试器。

**断言**并**ASSERTMSG**是仅在已检验的版本环境中编译时为活动状态。 编译时可用的生成环境中，它们会产生任何影响。

这些例程，以及生成环境的完整文档，请参阅 Windows 驱动程序工具包。

 

 





