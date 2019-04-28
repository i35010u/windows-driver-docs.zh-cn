---
title: 调试 WinLogon
description: 调试 WinLogon
ms.assetid: 408727cd-fb59-44fe-b896-88317d2bc087
keywords:
- WinLogon 调试
- NTSD，调试 CSRSS
- 控制用户模式下的调试程序与内核调试器，调试 WinLogon
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c82afa9cd90ae707e4046d816f38771818ae4fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346338"
---
# <a name="debugging-winlogon"></a>调试 WinLogon


## <span id="ddk_debugging_winlogon_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_WINLOGON_WITH_NTSD_DBG"></span>


WinLogon 是用户模式进程，用于处理该任务的交互式用户登录和注销，并处理 CTRL + ALT + DELETE 的所有实例。

### <a name="span-idcontrollingntsdfromthekerneldebuggerspanspan-idcontrollingntsdfromthekerneldebuggerspancontrolling-ntsd-from-the-kernel-debugger"></a><span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试程序的控制 NTSD

若要调试 WinLogon 的最简单方法是使用 NTSD 并[控件从内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

### <a name="span-idenablingwinlogondebuggingspanspan-idenablingwinlogondebuggingspanenabling-winlogon-debugging"></a><span id="enabling_winlogon_debugging"></span><span id="ENABLING_WINLOGON_DEBUGGING"></span>启用调试 WinLogon

因为您将为用户模式下调试程序将输出重定向到内核调试程序，需要设置内核调试连接。 请参阅[设置为调试](getting-set-up-for-debugging.md)。

若要将调试器附加到 WinLogon，则必须经过注册表以便从其启动的时调试该进程。 若要设置 WinLogon 调试，设置**HKEY\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\图像文件执行选项\\WinLogon.EXE\\调试器**到：

```console
ntsd -d -x -g 
```

**-D**选项将控制传递到内核调试程序。 **-X**选项会导致调试器捕获访问冲突作为第二个可能的异常。 **-G**选项将使 WinLogon 进程附件之后运行。 不要将添加 **-g**如果想要开始调试之前 Winlogon.exe 开始 （例如，如果您想要设置初始断点）。

此外，应设置下的 GlobalFlag 值**winlogon.exe**密钥 REG\_DWORD"0x000400F0"。 这将设置堆检查和 FLG\_启用\_KDEBUG\_符号\_负载。 但是，由于此第二个标志仅影响内核调试程序，或必须还将符号复制到目标计算机启动调试器之前。

注册表更改需要重新启动才能生效。

### <a name="span-idperformingthedebuggingspanspan-idperformingthedebuggingspanperforming-the-debugging"></a><span id="performing_the_debugging"></span><span id="PERFORMING_THE_DEBUGGING"></span>执行的调试

下一步重新启动后，调试器将中断到 WinLogon 自动。

请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关如何继续的说明。

你将需要设置符号路径为主机计算机上的位置或在网络上的其他某个位置。 当正在调试 WinLogon 时，目标计算机上的网络身份验证将无法正常工作。

 

 





