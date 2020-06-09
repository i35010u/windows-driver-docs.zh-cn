---
title: 本地内核模式调试
description: 本地内核模式调试
ms.assetid: e66dc23b-9254-4148-9828-d27c30bfa492
keywords:
- 本地内核调试
- 本地内核调试，可用命令
- 本地内核调试，LiveKD 工具
- LiveKD 工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81f3681d73140c4bf897e8c3adddc7620c4a1ec
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534448"
---
# <a name="local-kernel-mode-debugging"></a>本地内核模式调试


适用于 Windows 的调试工具支持*本地内核调试*。 这是一台计算机上的内核模式调试。 换句话说，调试器在正在调试的同一台计算机上运行。

## <a name="span-idstarting_local_kernel_debuggingspanspan-idstarting_local_kernel_debuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>设置本地内核模式调试


有关设置本地内核模式调试的信息，请参阅[手动设置单台计算机的本地内核模式调试](setting-up-local-kernel-debugging-of-a-single-computer-manually.md)。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

以管理员身份打开 WinDbg。 在 "**文件**" 菜单上，选择 "**内核调试**"。 在 "内核调试" 对话框中，打开 "**本地**" 选项卡。单击 **"确定"**。

还可以通过以管理员身份打开命令提示符窗口并输入以下命令来启动与 WinDbg 的会话：

**windbg-kl**

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

以管理员身份打开命令提示符窗口，然后输入以下命令：

**kd-kl**

## <a name="span-idcommands_that_are_not_availablespanspan-idcommands_that_are_not_availablespancommands-that-are-not-available"></a><span id="commands_that_are_not_available"></span><span id="COMMANDS_THAT_ARE_NOT_AVAILABLE"></span>不可用的命令


并非所有命令在本地内核调试会话中都可用。 通常，您不能使用导致目标计算机停止的任何命令，即使您无法恢复操作。

特别是，不能使用以下命令：

-   执行命令，如**g （走）**、 **p （Step）**、 **t （Trace）**、 **wt （跟踪和监视数据）**、 **tb （跟踪到下一个分支）**、 **Gh （处理异常**情况）和**gn （未处理异常）**

-   关闭和转储文件命令，例如，**崩溃**、**转储**和**重新启动**

-   断点命令，如**bp**、 **bu**、 **ba**、 **bc**、 **bd**、as **be**和**bl**

-   注册显示命令，如**r**和变体

-   堆栈跟踪命令，如**k**和变体

如果使用 WinDbg 执行本地内核调试，则所有的等效菜单命令和按钮也不可用。

## <a name="span-idcommands_that_are_availablespanspan-idcommands_that_are_availablespancommands-that-are-available"></a><span id="commands_that_are_available"></span><span id="COMMANDS_THAT_ARE_AVAILABLE"></span>可用的命令


所有内存输入和输出命令都可用。 你可以从用户内存和内核内存中自由读取。 还可以写入内存。 请确保不会写入核心内存的错误部分，因为它可能会损坏数据结构，并经常导致计算机停止响应（即*崩溃*）。

## <a name="span-iddifficulties_in_performing_local_kernel_debuggingspanspan-iddifficulties_in_performing_local_kernel_debuggingspandifficulties-in-performing-local-kernel-debugging"></a><span id="difficulties_in_performing_local_kernel_debugging"></span><span id="DIFFICULTIES_IN_PERFORMING_LOCAL_KERNEL_DEBUGGING"></span>执行本地内核调试的难点


本地内核调试是一种非常微妙的操作。 请注意，不会损坏或崩溃系统。

本地内核调试最困难的一个方面是计算机状态不断变化。 内存分页进和输出，活动进程会不断变化，并且虚拟地址上下文不会保持不变。 但在这些情况下，您可以有效地分析更改速度较慢的事件，例如某些设备状态。

内核模式驱动程序和 Windows 操作系统使用**DbgPrint**和相关函数经常向内核调试器发送消息。 在本地内核调试过程中不会自动显示这些消息。 可以使用[**！ dbgprint**](-dbgprint.md)扩展来显示它们。

## <a name="span-idlivekdspanspan-idlivekdspanlivekd"></a><span id="livekd"></span><span id="LIVEKD"></span>LiveKD


LiveKD 工具模拟本地内核调试。 此工具创建内核内存的 "快照" 转储文件，而不会在创建此快照时实际停止内核。 （因此，快照实际上可能并不显示计算机的单个即时状态。）

LiveKD 不是 Windows 包调试工具的一部分。 可以从 Windows Sysinternals 站点下载[LiveKd](https://docs.microsoft.com/sysinternals/downloads/livekd) 。

 

 





