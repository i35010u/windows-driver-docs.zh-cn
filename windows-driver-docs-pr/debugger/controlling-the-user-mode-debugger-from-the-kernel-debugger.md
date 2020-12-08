---
title: 通过内核调试程序控制用户模式调试程序
description: 通过内核调试程序控制用户模式调试程序
keywords:
- KD，控制 CDB 或 NTSD
- WinDbg，控制 CDB 或 NTSD
- CDB，将控制重定向到内核调试器
- NTSD，将控件重定向到内核调试器
- 将用户模式输出重定向到内核调试器
- 从内核调试器控制用户模式调试器
- 从内核调试器控制用户模式调试器，概述
- 从内核调试器、睡眠模式控制用户模式调试器
- 睡眠模式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 822407bc6b0241a28f9563eafb37f8e02456e721
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833691"
---
# <a name="controlling-the-user-mode-debugger-from-the-kernel-debugger"></a>通过内核调试程序控制用户模式调试程序


## <span id="ddk_controlling_the_user_mode_debugger_from_the_kernel_debugger_dbg"></span><span id="DDK_CONTROLLING_THE_USER_MODE_DEBUGGER_FROM_THE_KERNEL_DEBUGGER_DBG"></span>


您可以将用户模式调试器的输入和输出重定向到内核调试器。 此重定向使内核调试器能够控制在目标计算机上发生的特定用户模式调试会话。

可以使用 KD 或 WinDbg 作为内核调试器。 请注意，在此方案中，很多熟悉的 WinDbg 功能均不可用。 例如，不能使用 "局部变量" 窗口、"反汇编" 窗口或 "调用堆栈" 窗口，也不能单步执行源代码。 这是因为，WinDbg 只充当在目标计算机上运行的调试程序 (NTSD 或 CDB) 的查看器。

可以使用 CDB 或 NTSD 作为用户模式调试器。 NTSD 是更好的选择，因为它需要对其应用程序进行调试的计算机的处理器和操作系统的资源降至最低。 事实上，在内核调试器控制下启动 NTSD 后，不会创建 NTSD 窗口。 使用 NTSD，你可以在启动阶段的早期通过串行端口执行用户模式调试，并延迟关机。

**注意**  将用户模式调试器的输出重定向到内核调试器时，不支持 [**shell**](-shell--command-shell-.md) 命令。

 

本节包括下列内容：

-   [启动调试会话](starting-the-debugging-session.md) 介绍了如何从内核调试器中开始控制用户模式调试器的会话。

-   [切换模式](switching-modes.md) 描述了所涉及的四种不同模式，以及如何在它们之间进行替换。

-   [何时使用此方法](when-to-use-this-technique.md) 介绍此方法特别有用的方案。

-   将[此方法与远程调试相结合](combining-this-method-with-remote-debugging.md)介绍了如何从内核调试器控制用户模式调试器，并同时将其用作调试服务器。 如果用户模式符号位于符号服务器上，此组合会很有用。

 

 





