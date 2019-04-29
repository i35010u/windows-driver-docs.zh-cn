---
title: B （Windows 调试器词汇表）
description: 术语表页-B
Robots: noindex, nofollow
ms.assetid: 5ba110fc-1a12-4cbd-adc9-ef9441e257cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23a9888c606525e9611a88f8fae4087c9ba0ceb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356679"
---
# <a name="b"></a>B


<span id="blue_screen"></span><span id="BLUE_SCREEN"></span>**蓝屏**  
显示的 bug 检查发生后的蓝色字符模式屏幕。

<span id="breakpoint"></span><span id="BREAKPOINT"></span>**breakpoint**  
目标或目标操作，这将导致触发时发生的事件中的位置。

有关详细信息，请参阅[使用断点](using-breakpoints.md)。

<span id="breakpoint_id"></span><span id="BREAKPOINT_ID"></span>**breakpoint ID**  
断点唯一标识符。

有关详细信息，请参阅[使用断点](using-breakpoints.md)。

<span id="breakpoint_type"></span><span id="BREAKPOINT_TYPE"></span>**断点类型**  
用来实现该断点的方法。 有两种类型的断点： 处理器断点和软件的断点。

<span id="break_status"></span><span id="BREAK_STATUS"></span>**中断状态**  
设置会影响如何事件后继续执行调试程序引擎。 中断状态指示是否应在调试器中中断事件，具有打印到调试器控制台的通知或被忽略。 中断状态是事件筛选器的一部分。

另请参阅[*处理状态*](h.md#handling-status)。

有关详细信息，请参阅主题[控制异常和事件](controlling-exceptions-and-events.md)并[事件筛选器](event-filters.md)。

<span id="bug_check"></span><span id="BUG_CHECK"></span>**bug 检查**  
当 Windows 遇到内所需的操作或其他严重错误，数据不一致的硬件问题时它关闭，并在蓝色的字符模式屏幕上显示错误的信息。

此关闭已知以不同方式为 bug 检查，内核错误，在系统发生崩溃，停止错误或，有时，捕获。 显示在屏幕自身称为蓝色屏幕或停止屏幕。 在屏幕上显示的最重要信息是可在发生崩溃; 有关信息的消息代码这称为错误检查代码或停止代码。

WinDbg 或 KD 可以配置系统，以便此类错误发生时，调试器将自动联系。 或者，可以指示系统会自动发生此类错误时重新启动。

有关详细信息，请参阅 [Bug 检查（蓝屏）](bug-checks--blue-screens-.md)。

<span id="bug_check_code"></span><span id="BUG_CHECK_CODE"></span>**错误检查代码**  
指示特定类型的 bug 的十六进制代码检查。

 

 





