---
title: 用户模式调试期间的安全性
description: 用户模式调试期间的安全性
keywords:
- 安全注意事项，用户模式调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ec446928d8ed9b48d78c8b5da061a40ac7a557
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795169"
---
# <a name="security-during-user-mode-debugging"></a>用户模式调试期间的安全性


## <span id="ddk_security_during_user_mode_debugging_dbg"></span><span id="DDK_SECURITY_DURING_USER_MODE_DEBUGGING_DBG"></span>


当用户模式调试器处于活动状态时，它可以有效地控制计算机上的任何进程。

在用户模式调试过程中可能会出现安全问题，有三种可能的方法：

-   如果你使用损坏或破坏性的扩展 Dll，它们可能会导致你的调试器执行意外的操作，可能会影响你的目标以外的应用程序。

-   损坏或破坏性符号文件可能还会导致调试器执行意外的操作，可能会影响目标以外的应用程序。

-   如果正在运行远程调试会话，则意外的客户端可能会尝试链接到您的服务器。 或者可能是您期望的客户端可能会尝试执行您未预期的操作。

有关如何防范意外远程连接的建议，请参阅 [远程调试过程中的安全性](security-during-remote-debugging.md)。 远程客户端加入用户模式调试会话之后，无法限制其对计算机上进程的访问。

如果未执行远程调试，则还应注意错误的符号文件和扩展 Dll。 不要加载您不信任的符号或扩展！

 

 





