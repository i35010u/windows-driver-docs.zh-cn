---
title: 手动设置一台计算机的本地内核调试
description: 手动设置一台计算机的本地内核调试
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f7ab248829a98479f1125faf11f2869b657b3789
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813981"
---
# <a name="setting-up-local-kernel-debugging-of-a-single-computer-manually"></a>手动设置一台计算机的本地内核调试


适用于 Windows 的调试工具支持 *本地内核调试*。 这是一台计算机上的内核模式调试。 换句话说，调试器在正在调试的同一台计算机上运行。 利用本地调试，可以检查状态，但不会中断会导致操作系统停止运行的内核模式进程。

*本地* bcdedit 选项在 windows 8.0 和 windows Server 2012 及更高版本中可用。

## <a name="span-idstarting_local_kernel_debuggingspanspan-idstarting_local_kernel_debuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>设置本地 Kernel-Mode 调试

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。 完成调试并在本地计算机上禁用内核调试之后，可以重新启用安全启动。  


1.  以管理员身份打开命令提示符窗口。 **在上输入 bcdedit/debug**
2.  如果计算机尚未配置为调试传输的目标，请输入 **bcdedit/dbgsettings local**
3.  重新启动计算机。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

以管理员身份打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **本地** " 选项卡。选择 **"确定"**。

还可以通过以管理员身份打开命令提示符窗口并输入以下命令来启动与 WinDbg 的会话：

**windbg-kl**

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

以管理员身份打开命令提示符窗口，然后输入以下命令：

**kd-kl**

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[本地内核模式调试](performing-local-kernel-debugging.md)

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






