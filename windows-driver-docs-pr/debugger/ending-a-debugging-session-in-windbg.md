---
title: 在 WinDbg 中结束调试会话
description: 在 WinDbg 中结束调试会话
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb55c0438a98a4e88db5293f34c03c66a266f4c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828237"
---
# <a name="ending-a-debugging-session-in-windbg"></a>在 WinDbg 中结束调试会话


## <a name="span-idexiting_windbgspanspan-idexiting_windbgspanspan-idexiting_windbgspanexiting-windbg"></a><span id="Exiting_WinDbg"></span><span id="exiting_windbg"></span><span id="EXITING_WINDBG"></span>正在退出 WinDbg


可以通过从 "**文件**" 菜单中选择 "**退出**" 或按 ALT + F4 来退出 WinDbg。

如果要执行用户模式调试，则这些命令会关闭正在调试的应用程序，除非在启动调试器时使用了 **-pd** 命令行选项。

如果正在执行内核模式调试，则目标计算机将保持其当前状态。 这种情况下，你可以使目标保持运行状态或冻结状态。  (如果将目标冻结，则从内核调试器进行的任何将来连接都可以在您离开它的位置继续调试。 ) 

## <a name="span-idending_a_user_mode_session_without_exitingspanspan-idending_a_user_mode_session_without_exitingspanending-a-user-mode-session-without-exiting"></a><span id="ending_a_user_mode_session_without_exiting"></span><span id="ENDING_A_USER_MODE_SESSION_WITHOUT_EXITING"></span>结束 User-Mode 会话但不退出


若要结束用户模式调试会话，请将调试器返回到休眠模式，然后关闭目标应用程序，可以使用以下方法：

-   输入 [**kill (Kill Process)**](-kill--kill-process-.md) 命令。

-   输入 [**q (Quit)**](q--qq--quit-.md) 命令 (，除非已通过 **-pd** 选项) 启动了调试器。

-   从 "**调试**" 菜单中选择 "**停止调试**"。
-   按 SHIFT + F5。

-   单击工具栏 **Stop Debugging** 上的 "停止 ![ 调试" 按钮 (屏幕截图 ](images/tbstop.png)) 上的 "停止调试" 按钮

若要结束用户模式调试会话，请将调试器返回到休眠模式，然后将目标应用程序设置为再次运行，可以使用以下方法：

-   输入 [**(从进程中分离的)**](-detach--detach-from-process-.md) "命令。 如果正在调试多个目标，则此命令从当前目标中分离，并继续与剩余目标的调试会话。

-   从 "**调试**" 菜单中选择 "**分离调试对象**"。 如果正在调试多个目标，则此命令将从所有当前目标中分离。

-   输入 [**qd (Quit 并分离)**](qd--quit-and-detach-.md) 命令。

-   如果已通过 **-pd** 选项启动调试器，请输入 [**q (Quit)**](q--qq--quit-.md)命令。

若要结束用户模式调试会话，请将调试器恢复到休眠模式，但使目标应用程序处于调试状态，可以使用以下方法：

-   输入 [**(放弃进程)**](-abandon--abandon-process-.md) 命令。

有关重新附加到目标的详细信息，请参阅重新 [附加到目标应用程序](reattaching-to-the-target-application.md)。

## <a name="span-idending_a_kernel-mode_session_without_exitingspanspan-idending_a_kernel-mode_session_without_exitingspanspan-idending_a_kernel-mode_session_without_exitingspanending-a-kernel-mode-session-without-exiting"></a><span id="Ending_a_Kernel-Mode_Session_Without_Exiting"></span><span id="ending_a_kernel-mode_session_without_exiting"></span><span id="ENDING_A_KERNEL-MODE_SESSION_WITHOUT_EXITING"></span>结束 Kernel-Mode 会话但不退出


若要结束内核模式调试会话，请将调试器恢复为休眠模式，并使目标计算机处于冻结状态，可以使用以下方法：

-   输入 [**q (Quit)**](q--qq--quit-.md) 命令 (，除非已通过 **-pd** 选项启动调试器) 

-   从 "**调试**" 菜单中选择 "**停止调试**"。
-   按 SHIFT + F5。

-   在工具栏上的 "停止调试" 按钮) ，单击 " **停止调试" (Shift + F5)** 按钮 (![ 屏幕截图 ](images/tbstop.png) 。

当某一 WinDbg 会话结束时，系统将提示您为当前会话保存工作区，而 WinDbg 返回到休眠模式。 此时，你可以使用所有启动选项。 也就是说，您可以开始调试正在运行的进程、生成新进程、附加到目标计算机、打开故障转储或连接到远程调试会话。

 

 





