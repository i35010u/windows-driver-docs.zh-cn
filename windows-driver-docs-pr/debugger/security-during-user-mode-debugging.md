---
title: 用户模式调试期间的安全性
description: 用户模式调试期间的安全性
ms.assetid: e198c29a-d793-4974-8ee3-f26679bd70b4
keywords:
- 安全注意事项，用户模式下调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f12e1df4c3f97408bc6c840177e3fc11597fbaee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381989"
---
# <a name="security-during-user-mode-debugging"></a>用户模式调试期间的安全性


## <span id="ddk_security_during_user_mode_debugging_dbg"></span><span id="DDK_SECURITY_DURING_USER_MODE_DEBUGGING_DBG"></span>


当用户模式下调试程序处于活动状态时，它可以有效地控制任何计算机上的进程。

有三种方法在用户模式下调试期间，可能会出现安全问题：

-   如果使用已损坏或破坏性扩展 Dll，它们可能会导致调试程序执行意外的操作，还可能会影响应用程序而非你的目标。

-   很可能已损坏或破坏性的符号文件也可能导致调试器执行意外的操作，还可能会影响应用程序而非你的目标。

-   如果运行远程调试会话时，发生意外客户端可能会尝试链接到你的服务器。 或者，可能是在需要在客户端可能会尝试执行未预计到的操作。

有关如何防范意外的远程连接的建议，请参阅[安全在远程调试](security-during-remote-debugging.md)。 远程客户端已加入一个用户模式下调试会话后，没有任何方法来限制其访问对您的计算机上的进程。

如果没有执行远程调试，你应仍请注意错误的符号文件和扩展 Dll。 无法加载符号或你不信任的扩展 ！

 

 





