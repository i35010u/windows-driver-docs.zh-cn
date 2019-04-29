---
title: 手动设置一台计算机的本地内核调试
description: 手动设置一台计算机的本地内核调试
ms.assetid: FC717B1C-A68A-4002-A528-BFC3521C5E8A
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c09ae58a59a182fbb01170a7402927b9dd88336
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374327"
---
# <a name="setting-up-local-kernel-debugging-of-a-single-computer-manually"></a>手动设置一台计算机的本地内核调试


调试工具的 Windows 支持*本地内核调试*。 这是一台计算机上的内核模式调试。 换而言之，调试器在正在调试的同一台计算机上运行。 使用本地调试，您可以检查状态，但不是会中断到内核模式进程会导致停止运行的操作系统。

*本地*bcdedit 选项是可用在 Windows 8.0 和 Windows Server 2012 及更高版本。

## <a name="span-idstartinglocalkerneldebuggingspanspan-idstartinglocalkerneldebuggingspansetting-up-local-kernel-mode-debugging"></a><span id="starting_local_kernel_debugging"></span><span id="STARTING_LOCAL_KERNEL_DEBUGGING"></span>设置本地的内核模式调试

> [!IMPORTANT]
> 使用 bcdedit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。 您可以重新启用安全启动完成后，调试和您禁用了内核调试本地计算机上。  


1.  以管理员身份打开命令提示符窗口。 输入**bcdedit /debug 上**
2.  如果计算机尚未配置为调试传输的目标，输入**bcdedit /dbgsettings 本地**
3.  重新启动计算机。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>使用 WinDbg

以管理员身份打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**本地**选项卡。单击“确定” 。

也可以使用 WinDbg 启动会话，通过打开管理员命令提示符窗口并输入以下命令：

**windbg -kl**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>使用 KD

打开命令提示符窗口，以管理员身份，并输入以下命令：

**kd -kl**

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[本地内核模式调试](performing-local-kernel-debugging.md)

[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






