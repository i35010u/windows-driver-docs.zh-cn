---
title: 内核模式调试期间的安全性
description: 内核模式调试期间的安全性
ms.assetid: 0dc78f83-a695-4b2c-a5cd-d7f365a9560f
keywords:
- 安全注意事项，内核模式调试
- 本地内核调试，安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4ee4b5b1da62391dfafdf226ceeaa3686364e1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381995"
---
# <a name="security-during-kernel-mode-debugging"></a>内核模式调试期间的安全性


## <span id="ddk_security_during_kernel_mode_debugging_dbg"></span><span id="DDK_SECURITY_DURING_KERNEL_MODE_DEBUGGING_DBG"></span>


内核模式调试过程中的安全性都是永远不会为了防止*目标*计算机。 目标是完全受到调试器--这是调试的本质。

如果在启动期间启用了调试连接，它将保持易受攻击的调试端口通过直到其下一次启动。

但是，你应会担心安全性*主机*计算机。 在理想情况下，调试器主机计算机时，作为应用程序运行，但不与此计算机上的其他应用程序交互。 有三种方法中的安全时出现问题：

-   如果使用已损坏或破坏性扩展 Dll，它们可能会导致调试程序执行意外的操作，还可能会影响主计算机。

-   很可能已损坏或破坏性的符号文件也可能导致调试器执行意外的操作，还可能会影响主计算机。

-   如果运行远程调试会话时，发生意外客户端可能会尝试链接到你的服务器。 或者，可能是在需要在客户端可能会尝试执行未预计到的操作。

如果你想要阻止远程用户执行的操作在主机上，使用[安全模式下](secure-mode.md)。

有关如何防范意外的远程连接的建议，请参阅[安全在远程调试](security-during-remote-debugging.md)。

如果没有执行远程调试，你应仍请注意错误的符号文件和扩展 Dll。 无法加载符号或你不信任的扩展 ！

### <a name="span-idlocalkerneldebuggingspanspan-idlocalkerneldebuggingspanlocal-kernel-debugging"></a><span id="local_kernel_debugging"></span><span id="LOCAL_KERNEL_DEBUGGING"></span>本地内核调试

只有拥有调试权限的用户可以启动本地内核调试会话。 如果你是具有多个用户帐户的计算机的管理员，你应注意具有这些权限的用户可以启动本地内核调试会话、 有效地为他们提供的所有进程的计算机--上的控件并因此给予它们访问权限以及所有外围设备。

 

 





