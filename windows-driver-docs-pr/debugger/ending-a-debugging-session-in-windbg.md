---
title: 在 WinDbg 中结束调试会话
description: 在 WinDbg 中结束调试会话
ms.assetid: 9C19211B-38CC-482B-B69F-B83B29963B3F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3406b5ecef7d23eb740093b99942bfdf382dd182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340599"
---
# <a name="ending-a-debugging-session-in-windbg"></a>在 WinDbg 中结束调试会话


## <a name="span-idexitingwindbgspanspan-idexitingwindbgspanspan-idexitingwindbgspanexiting-windbg"></a><span id="Exiting_WinDbg"></span><span id="exiting_windbg"></span><span id="EXITING_WINDBG"></span>退出 WinDbg


可以通过选择退出 WinDbg**退出**从**文件**菜单或通过按 alt+f4。

如果您正在执行用户模式下调试，这些命令将关闭正在调试的应用程序，除非您使用，否则 **-pd**启动调试器时的命令行选项。

如果您正在执行内核模式调试，目标计算机保持在其当前状态。 这种情况下，可让目标保留正在运行或已冻结。 （如果将冻结的目标，从内核调试程序的任何未来连接可以继续调试您离开的位置。）

## <a name="span-idendingausermodesessionwithoutexitingspanspan-idendingausermodesessionwithoutexitingspanending-a-user-mode-session-without-exiting"></a><span id="ending_a_user_mode_session_without_exiting"></span><span id="ENDING_A_USER_MODE_SESSION_WITHOUT_EXITING"></span>但不退出结束用户模式会话


若要结束用户模式下调试会话，请返回到休眠模式下，调试器和关闭目标应用程序，可以使用以下方法：

-   输入[ **.kill （终止进程）** ](-kill--kill-process-.md)命令。

-   输入[ **q (Quit)** ](q--qq--quit-.md)命令 (除非启动的调试器 **-pd**选项)。

-   选择**停止调试**从**调试**菜单。
-   按 SHIFT + F5。

-   单击**停止调试**按钮 (![停止调试按钮的屏幕截图](images/tbstop.png)) 工具栏上

若要结束用户模式下调试会话，请为休眠模式中，并再次运行目标应用程序的情况下，可以使用以下方法将返回调试器：

-   输入[ **.detach （与进程分离）** ](-detach--detach-from-process-.md)命令。 如果你正在调试多个目标，此命令将当前目标从分离，并将剩余目标的调试会话继续。

-   选择**分离调试对象**从**调试**菜单。 如果你正在调试多个目标，此命令将从所有当前目标分离。

-   输入[ **qd （Quit 和分离）** ](qd--quit-and-detach-.md)命令。

-   输入[ **q (Quit)** ](q--qq--quit-.md)命令时，如果启动的调试器 **-pd**选项。

若要用户模式下调试会话结束，返回调试器到休眠模式，但使目标应用程序处于调试状态，可以使用以下方法：

-   输入[ **.abandon （放弃进程）** ](-abandon--abandon-process-.md)命令。

有关重新附加到目标的信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

## <a name="span-idendingakernel-modesessionwithoutexitingspanspan-idendingakernel-modesessionwithoutexitingspanspan-idendingakernel-modesessionwithoutexitingspanending-a-kernel-mode-session-without-exiting"></a><span id="Ending_a_Kernel-Mode_Session_Without_Exiting"></span><span id="ending_a_kernel-mode_session_without_exiting"></span><span id="ENDING_A_KERNEL-MODE_SESSION_WITHOUT_EXITING"></span>但不退出结束的内核模式会话


若要结束的内核模式调试会话，返回到休眠模式下，调试器并保留冻结的目标计算机，可以使用以下方法：

-   输入[ **q (Quit)** ](q--qq--quit-.md)命令 (除非启动的调试器 **-pd**选项)

-   选择**停止调试**从**调试**菜单。
-   按 SHIFT + F5。

-   单击**停止调试 (Shift + F5)** 按钮 (![停止调试按钮的屏幕截图](images/tbstop.png)) 工具栏上。

WinDbg 会话结束时，系统会提示为当前会话中，保存工作区，WinDbg 然后返回到休眠模式。 此时，你可以使用所有起始选项。 也就是说，您可以开始调试正在运行的进程、 生成新的进程、 将附加到目标计算机，打开故障转储，或连接到远程调试会话。

 

 





