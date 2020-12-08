---
title: 内核模式调试期间的安全性
description: 内核模式调试期间的安全性
keywords:
- 安全注意事项，内核模式调试
- 本地内核调试，安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f8c534ff7abc4a22ae5778566e3e529f92c820
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839937"
---
# <a name="security-during-kernel-mode-debugging"></a>内核模式调试期间的安全性


## <span id="ddk_security_during_kernel_mode_debugging_dbg"></span><span id="DDK_SECURITY_DURING_KERNEL_MODE_DEBUGGING_DBG"></span>


内核模式调试过程中的安全性决不会保护 *目标* 计算机。 目标完全容易出现在调试器中，这是调试的本质。

如果在启动过程中启用了调试连接，则在下一次启动之前，它将一直受到调试端口的攻击。

但是，你应该关心 *主* 计算机上的安全性。 在理想情况下，调试器作为主计算机上的应用程序运行，但不与此计算机上的其他应用程序交互。 有三种可能出现安全问题的方法：

-   如果使用损坏或破坏性的扩展 Dll，它们可能会导致调试器执行意外的操作，可能会影响主机计算机。

-   损坏或破坏性符号文件可能还会导致调试器执行意外的操作，可能会影响主机计算机。

-   如果正在运行远程调试会话，则意外的客户端可能会尝试链接到您的服务器。 或者可能是您期望的客户端可能会尝试执行您未预期的操作。

如果要阻止远程用户在主计算机上执行操作，请使用 [安全模式](secure-mode.md)。

有关如何防范意外远程连接的建议，请参阅 [远程调试过程中的安全性](security-during-remote-debugging.md)。

如果未执行远程调试，则还应注意错误的符号文件和扩展 Dll。 不要加载您不信任的符号或扩展！

### <a name="span-idlocal_kernel_debuggingspanspan-idlocal_kernel_debuggingspanlocal-kernel-debugging"></a><span id="local_kernel_debugging"></span><span id="LOCAL_KERNEL_DEBUGGING"></span>本地内核调试

只有具有调试权限的用户才能启动本地内核调试会话。 如果你是具有多个用户帐户的计算机的管理员，则你应注意具有这些权限的任何用户都可以启动本地内核调试会话，从而有效地为其提供对计算机上所有进程的控制，从而为他们提供对所有外围设备的访问权限。

 

 





