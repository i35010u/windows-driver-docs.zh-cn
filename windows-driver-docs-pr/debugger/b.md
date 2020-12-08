---
title: 'B (Windows 调试器词汇表) '
description: 词汇表页-B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94a586576cbab04d4bcb1c42bd53904b1900904
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819287"
---
# <a name="b"></a>B


<span id="blue_screen"></span><span id="BLUE_SCREEN"></span>**蓝屏**  
发生 bug 检查后显示的蓝色字符模式屏幕。

<span id="breakpoint"></span><span id="BREAKPOINT"></span>**逐**  
目标或目标操作中的一个位置，该位置将在触发时引发事件。

有关详细信息，请参阅 [使用断点](using-breakpoints.md)。

<span id="breakpoint_id"></span><span id="BREAKPOINT_ID"></span>**断点 ID**  
断点的唯一标识符。

有关详细信息，请参阅 [使用断点](using-breakpoints.md)。

<span id="breakpoint_type"></span><span id="BREAKPOINT_TYPE"></span>**断点类型**  
用于实现断点的方法。 有两种类型的断点：处理器断点和软件断点。

<span id="break_status"></span><span id="BREAK_STATUS"></span>**中断状态**  
影响调试器引擎在事件完成后如何继续的设置。 中断状态指示事件是应中断到调试器、将通知打印到调试器控制台还是被忽略。 中断状态是事件筛选器的一部分。

另请参阅 [*处理状态*](h.md#handling-status)。

有关详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md) 和 [事件筛选器](event-filters.md)的主题。

<span id="bug_check"></span><span id="BUG_CHECK"></span>**bug 检查**  
当 Windows 遇到硬件问题、其操作所需的数据不一致或其他严重错误时，它会关闭并在蓝色字符模式屏幕上显示错误信息。

此关闭被称为 "bug 检查"、"内核错误"、"系统崩溃"、"停止错误" 或 "偶尔" 陷阱。 屏幕显示本身称为蓝屏或停止屏幕。 屏幕上显示的最重要信息是一条消息代码，提供有关故障的信息;这称为 "bug 检查代码" 或 "停止代码"。

WinDbg 或 KD 可以对系统进行配置，以便在发生此类错误时自动联系到调试器。 或者，可以指示系统在发生此类错误时自动重新启动。

有关详细信息，请参阅 [Bug 检查（蓝屏）](bug-checks--blue-screens-.md)。

<span id="bug_check_code"></span><span id="BUG_CHECK_CODE"></span>**bug 检查代码**  
指示特定类型 bug 检查的十六进制代码。

 

 





