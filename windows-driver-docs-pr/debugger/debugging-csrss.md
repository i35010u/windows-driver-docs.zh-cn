---
title: 调试 CSRSS
description: 调试 CSRSS
keywords:
- CSRSS 调试
- NTSD，调试 CSRSS
- 从内核调试器控制用户模式调试器，调试 CSRSS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2859cbb97c47e8ed61b476832f1b85ec977d5fc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817535"
---
# <a name="debugging-csrss"></a>调试 CSRSS


## <span id="ddk_debugging_csrss_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_CSRSS_WITH_NTSD_DBG"></span>


客户端服务器 Run-Time 子系统 (CSRSS) 是控制 Windows 环境的基础层的用户模式进程。 有很多问题需要调试 CSRSS 本身。

如果 Windows 子系统意外终止，并出现 [**Bug 检查 0xc000021a**](bug-check-0xc000021a--winlogin-fatal-error.md) (WINLOGON \_ 严重错误) ，则调试 CSRSS 也很有用 \_ 。 在这种情况下，调试 CSRSS 将捕获到 "意外" 点之前出现的故障。

### <a name="span-idcontrolling_ntsd_from_the_kernel_debuggerspanspan-idcontrolling_ntsd_from_the_kernel_debuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试器控制 NTSD

调试 CSRSS 的最简单方法是使用 NTSD，并 [从内核调试器进行控制](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

### <a name="span-idenabling_csrss_debuggingspanspan-idenabling_csrss_debuggingspanenabling-csrss-debugging"></a><span id="enabling_csrss_debugging"></span><span id="ENABLING_CSRSS_DEBUGGING"></span>启用 CSRSS 调试

必须先启用 CSRSS 调试，然后才能继续。 如果目标计算机正在运行 Windows 的 *免费版本* ，则必须通过全局标志实用程序 (GFlags) 启用 CSRSS 调试。

为此，请启动 GFlags 实用工具，选择 **系统注册表** 单选按钮，然后选择 " **启用 Win32 子系统调试**"。

或者，可以使用以下 GFlags 命令行：

```dbgcmd
gflags /r +20000 
```

或者，如果愿意，可以手动编辑注册表项，而不是使用 GFlags。 打开以下注册表项：

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 
```

编辑 **GlobalFlag** 值条目 (类型为 REG \_ DWORD) ，并设置位0x00020000。

使用 GFlags 或手动编辑注册表后，必须重新启动才能使更改生效。

### <a name="span-idstarting_ntsdspanspan-idstarting_ntsdspanstarting-ntsd"></a><span id="starting_ntsd"></span><span id="STARTING_NTSD"></span>启动 NTSD

由于将从内核调试器控制用户模式调试器，因此需要设置内核调试连接。 有关详细信息，请参阅 [获取调试设置](getting-set-up-for-debugging.md) 。

正确配置注册表后，只需启动 NTSD 即可，如下所示：

**ntsd--**

有关如何继续的说明，请参阅 [控制内核调试器中的 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) 。

您必须将符号路径设置为主计算机上的某个位置或网络上的其他某个位置。 当调试 CSRSS 时，目标计算机上的网络身份验证将无法正常工作。

请注意，可能会看到 "页面 io 错误" 消息。 这是硬件故障的另一个表现形式。

当调试会话结束时，调试程序将从 CSRSS 分离，同时 CSRSS 进程仍在运行。 这样可以避免终止 CSRSS 进程本身。

 

 





