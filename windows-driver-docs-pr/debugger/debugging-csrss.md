---
title: 调试 CSRSS
description: 调试 CSRSS
ms.assetid: 9c3a8498-d9e4-4070-aee8-c038fa1666a4
keywords:
- CSRSS 调试
- NTSD，调试 CSRSS
- 控制用户模式下的调试程序与内核调试器，调试 CSRSS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2527c1f4b07f7f73a27fcde1b3eda6d91c27e528
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377186"
---
# <a name="debugging-csrss"></a>调试 CSRSS


## <span id="ddk_debugging_csrss_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_CSRSS_WITH_NTSD_DBG"></span>


客户端服务器运行时子系统 (CSRSS) 是控制 Windows 环境的基础层的用户模式进程。 有许多使调试 CSRSS 本身所需的问题。

调试 CSRSS 时也是有用的 Windows 子系统意外终止[ **Bug 检查 0xC000021A** ](bug-check-0xc000021a--status-system-process-terminated.md) (状态\_系统\_过程\_终止）。 在这种情况下，调试 CSRSS 会捕获失败之前就"意外"点。

### <a name="span-idcontrollingntsdfromthekerneldebuggerspanspan-idcontrollingntsdfromthekerneldebuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试程序的控制 NTSD

若要调试 CSRSS 的最简单方法是使用 NTSD 并[控件从内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

### <a name="span-idenablingcsrssdebuggingspanspan-idenablingcsrssdebuggingspanenabling-csrss-debugging"></a><span id="enabling_csrss_debugging"></span><span id="ENABLING_CSRSS_DEBUGGING"></span>启用 CSRSS 调试

必须启用 CSRSS 调试，然后才能继续运行。 如果目标计算机正在运行*已检验版本*的 Windows，CSRSS 调试始终处于启用状态。 如果目标计算机正在运行*免费生成*的 Windows，您将需要启用 CSRSS 调试通过 Global Flags Utility (GFlags)。

若要执行此操作，启动 GFlags 实用程序，选择**系统注册表**单选按钮，然后选择**启用调试 Win32 子系统的**。

或者，可以使用以下的 GFlags 命令行：

```dbgcmd
gflags /r +20000 
```

或者，如果您愿意，可以编辑手动而不是使用 GFlags 的注册表项。 打开以下注册表项：

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 
```

编辑**GlobalFlag**值项目 (类型 REG 的\_DWORD) 并将位 0x00020000 设置。

使用 GFlags 或手动编辑注册表之后, 您必须重新启动计算机更改才能生效。

### <a name="span-idstartingntsdspanspan-idstartingntsdspanstarting-ntsd"></a><span id="starting_ntsd"></span><span id="STARTING_NTSD"></span>起始 NTSD

因为您将控制用户模式下的调试程序与内核调试程序，需要设置内核调试连接。 请参阅[获取设置以便进行调试](getting-set-up-for-debugging.md)有关详细信息。

已正确配置注册表后，很简单，只需启动 NTSD，如下所示：

**ntsd --**

请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关如何继续的说明。

你将需要设置符号路径为主机计算机上的位置或在网络上的其他某个位置。 当正在调试 CSRSS 时，目标计算机上的网络身份验证将无法正常工作。

请注意，可能会看到"页面中的 io 错误"消息。 这是另一个实例化的硬件故障。

调试会话结束时，调试器将分离从 CSRSS CSRSS 进程仍在运行时。 这样可避免终止 CSRSS 进程本身。

 

 





