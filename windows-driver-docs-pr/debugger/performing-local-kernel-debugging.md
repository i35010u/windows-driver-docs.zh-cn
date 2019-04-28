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
ms.openlocfilehash: 755e0abd8fa9b095a81f7837a922dbf4988c4937
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352899"
---
# <a name="local-kernel-mode-debugging"></a>本地内核模式调试


调试工具的 Windows 支持*本地内核调试*。 这是一台计算机上的内核模式调试。 换而言之，调试器在正在调试的同一台计算机上运行。

## <a name="span-idstartinglocalkerneldebuggingspanspan-idstartinglocalkerneldebuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>设置本地的内核模式调试


有关设置本地的内核模式调试的信息，请参阅[设置本地内核模式调试的单个计算机手动](setting-up-local-kernel-debugging-of-a-single-computer-manually.md)。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

以管理员身份打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**本地**选项卡。单击“确定” 。

也可以使用 WinDbg 启动会话，通过打开管理员命令提示符窗口并输入以下命令：

**windbg -kl**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

打开命令提示符窗口，以管理员身份，并输入以下命令：

**kd -kl**

## <a name="span-idcommandsthatarenotavailablespanspan-idcommandsthatarenotavailablespancommands-that-are-not-available"></a><span id="commands_that_are_not_available"></span><span id="COMMANDS_THAT_ARE_NOT_AVAILABLE"></span>将不可用的命令


在本地的内核调试会话中提供了不是所有命令。 通常情况下，不能使用任何命令，因为不能恢复操作将导致停止，甚至暂时不可用，目标计算机。

具体而言，不能使用以下命令：

-   执行命令，如**g （转向）**， **p （步骤）**， **t (Trace)**， **wt （跟踪和查看数据）**， **tb （跟踪到下一步分支）**， **gh （转到异常处理）**，和**gn (Go 出现未处理的异常)**

-   关闭和转储文件命令，如 **.crash**， **.dump**，和 **.reboot**

-   断点命令，如**bp**， **bu**， **ba**， **bc**， **bd**，**是**，和**bl**

-   注册显示命令，如**r**和变体

-   堆栈跟踪命令，如**k**和变体

如果您正在执行本地内核使用 WinDbg 进行调试，所有等效的菜单命令和按钮都还不可用。

## <a name="span-idcommandsthatareavailablespanspan-idcommandsthatareavailablespancommands-that-are-available"></a><span id="commands_that_are_available"></span><span id="COMMANDS_THAT_ARE_AVAILABLE"></span>可用命令


所有内存都输入和输出命令可用。 你可以自由地阅读用户内存和内核内存中。 也可以写入内存。 请确保，你未写入到的错误的部件的内核内存，因为它可能会损坏数据结构，并经常导致计算机停止响应 (即*崩溃*)。

## <a name="span-iddifficultiesinperforminglocalkerneldebuggingspanspan-iddifficultiesinperforminglocalkerneldebuggingspandifficulties-in-performing-local-kernel-debugging"></a><span id="difficulties_in_performing_local_kernel_debugging"></span><span id="DIFFICULTIES_IN_PERFORMING_LOCAL_KERNEL_DEBUGGING"></span>在执行本地内核调试的问题


本地内核调试是非常细致的操作。 请注意，不会损坏或导致系统崩溃。

本地内核调试的最困难的方面之一是不断变化的计算机状态。 内存分页入和签出、 活动进程的不断更改以及虚拟地址上下文不执行保持不变。 但是，上述情况下，您可以有效地分析变化缓慢，例如，某些设备状态的操作。

内核模式驱动程序和 Windows 操作系统频繁地将消息发送到内核调试程序通过使用**DbgPrint**和相关函数。 本地内核调试期间不会自动显示这些消息。 可以使用显示它们[ **！ dbgprint** ](-dbgprint.md)扩展。

## <a name="span-idlivekdspanspan-idlivekdspanlivekd"></a><span id="livekd"></span><span id="LIVEKD"></span>LiveKD


LiveKD 工具来模拟本地内核调试。 此工具创建而无需进行此快照时实际停止内核的内核内存中，"快照"转储文件。 （因此，快照可能不实际显示单个即时状态的计算机。）

LiveKD 不是有关 Windows 调试工具软件包的一部分。 您可以下载[LiveKd](https://go.microsoft.com/fwlink/p/?linkid=56552)从 Windows Sysinternals 站点。

 

 





