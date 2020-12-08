---
title: 调试 WinLogon
description: 调试 WinLogon
keywords:
- WinLogon 调试
- NTSD，调试 CSRSS
- 从内核调试器控制用户模式调试器，调试 WinLogon
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef071a98a0bf0653b77a0e4bd742556aa71bf04e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785281"
---
# <a name="debugging-winlogon"></a>调试 WinLogon


## <span id="ddk_debugging_winlogon_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_WINLOGON_WITH_NTSD_DBG"></span>


WinLogon 是处理交互式用户登录和注销的任务，并处理 CTRL + ALT + DELETE 的所有实例的用户模式进程。

### <a name="span-idcontrolling_ntsd_from_the_kernel_debuggerspanspan-idcontrolling_ntsd_from_the_kernel_debuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试器控制 NTSD

调试 WinLogon 的最简单方法是使用 NTSD，并 [从内核调试器进行控制](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

### <a name="span-idenabling_winlogon_debuggingspanspan-idenabling_winlogon_debuggingspanenabling-winlogon-debugging"></a><span id="enabling_winlogon_debugging"></span><span id="ENABLING_WINLOGON_DEBUGGING"></span>启用 WinLogon 调试

由于要将用户模式调试器输出重定向到内核调试器，因此需要设置内核调试连接。 请参阅 [获取调试的设置](getting-set-up-for-debugging.md)。

若要将调试程序附加到 WinLogon，你必须通过注册表，以便在进程启动时进行调试。 若要设置 WinLogon 调试，请将 **HKEY \_ LOCAL \_ MACHINE \\ Software \\ Microsoft \\ Windows NT \\ CurrentVersion \\ Image File 执行选项设置 \\WinLogon.EXE\\ 调试程序** ，以：

```console
ntsd -d -x -g 
```

**-D** 选项将控制传递给内核调试器。 **-X** 选项会使调试器捕获访问冲突作为第二次异常。 **-G** 选项导致 WinLogon 进程在附件之后运行。 如果要在 Winlogon.exe 开始之前开始调试，请不要添加 **-g** (例如，如果想要) 设置初始断点。

此外，应将 **winlogon.exe** 项下的 GlobalFlag 值设置为 \_ "0x000400F0"。 这将设置堆检查并 FLG \_ 启用 \_ KDEBUG \_ 符号 \_ 加载。 但是，由于此第二个标志仅影响内核调试器，因此在启动调试器之前，还必须将符号复制到目标计算机。

注册表更改需要重新启动才能生效。

### <a name="span-idperforming_the_debuggingspanspan-idperforming_the_debuggingspanperforming-the-debugging"></a><span id="performing_the_debugging"></span><span id="PERFORMING_THE_DEBUGGING"></span>执行调试

下次重新启动后，调试器会自动中断 WinLogon。

有关如何继续的说明，请参阅 [控制内核调试器中的 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) 。

您必须将符号路径设置为主计算机上的某个位置或网络上的其他某个位置。 当调试 WinLogon 时，目标计算机上的网络身份验证将无法正常运行。

 

 





