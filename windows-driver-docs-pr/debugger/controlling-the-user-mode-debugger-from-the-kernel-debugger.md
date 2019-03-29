---
title: 通过内核调试程序控制用户模式调试程序
description: 通过内核调试程序控制用户模式调试程序
ms.assetid: 8fba2187-cf22-41ad-9b06-228a5b082822
keywords:
- KD、 CDB 或 NTSD 控制
- WinDbg、 CDB 或 NTSD 控制
- CDB，将控件重定向到内核调试程序
- NTSD，将控件重定向到内核调试程序
- 将用户模式下输出重定向到内核调试程序
- 控制用户模式下的调试程序与内核调试程序
- 控制用户模式下的调试程序与内核调试器中，概述
- 控制用户模式下的调试程序与内核调试器，睡眠模式
- 睡眠模式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: efeb46b14ac40f36e972cb474746dfaf58f4a627
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562632"
---
# <a name="controlling-the-user-mode-debugger-from-the-kernel-debugger"></a>通过内核调试程序控制用户模式调试程序


## <span id="ddk_controlling_the_user_mode_debugger_from_the_kernel_debugger_dbg"></span><span id="DDK_CONTROLLING_THE_USER_MODE_DEBUGGER_FROM_THE_KERNEL_DEBUGGER_DBG"></span>


您可以重定向输入和输出从用户模式下调试器到内核调试程序。 这种重定向启用内核调试程序，以控制特定的用户模式下调试会话的目标计算机上发生。

可以使用 KD 或 WinDbg，作为内核调试程序。 请注意，许多 WinDbg 的常见功能不在此方案中可用。 例如，无法使用局部变量窗口、 反汇编窗口中或调用堆栈窗口中，并且不能单步执行源代码。 这是因为 WinDbg 仅作为调试器 （NTSD 或 CDB） 的查看者在目标计算机上运行。

可以使用 CDB 或 NTSD，作为用户模式下调试程序。 NTSD 是计算机的更好的选择，因为它需要从处理器和操作系统正在调试的应用程序的最少的资源。 实际上，当 NTSD 受控制的内核调试程序启动时，都会创建没有 NTSD 窗口。 使用 NTSD，可以关闭到执行用户模式调试通过串行端口在启动阶段的早期和后期。

**请注意**   [ **.shell** ](-shell--command-shell-.md)用户模式下调试程序的输出重定向到内核调试程序时，不支持命令。

 

本部分包含下列内容：

-   [启动调试会话](starting-the-debugging-session.md)介绍了如何开始的会话的用户模式下调试程序控制从内核调试程序。

-   [切换模式](switching-modes.md)描述所涉及的四种不同模式以及它们之间进行交替。

-   [何时使用此技术](when-to-use-this-technique.md)介绍这种方法是特别有用的方案。

-   [将此方法与远程调试](combining-this-method-with-remote-debugging.md)介绍如何控制用户模式下的调试程序与内核调试程序，并在同一时间将其用作调试服务器。 此组合可以是用户模式符号位于符号服务器上的情况下很有用。

 

 





