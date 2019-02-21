---
title: 启动调试会话
description: 启动调试会话
ms.assetid: 789c61cf-edd2-4354-91a8-87a0a7af28a3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d46944dc9ab0a023a90198f527b5bace5be7d139
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519624"
---
# <a name="starting-the-debugging-session"></a>启动调试会话


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


在本文档中的如何[控制用户模式下从内核调试程序调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，*应用程序的目标*正在调试的用户模式应用程序是指*目标计算机*指的是包含目标应用程序和 NTSD 或 CDB 进程的计算机和*主机计算机*指包含内核调试程序的计算机。

若要开始使用这种方法，您必须执行以下操作。 你可以执行步骤 1 和 2 以任意顺序。

1. 使用-d 的命令行选项对目标计算机上启动 NTSD 或 CDB。

   例如，您可以将附加到正在运行的进程使用以下语法。

   **ntsd-d \[-y** <em>UserSymbolPath</em>  **\] -p** *PID*

   或者，可以通过使用以下语法为目标中开始一个新的进程。

   **ntsd -d \[-y** <em>UserSymbolPath</em>**\]** *ApplicationName*

   如果您正在安装这作为事后调试程序，将使用以下语法。

   **ntsd -d \[-y** <em>UserSymbolPath</em>**\]**

   有关此步骤的详细信息，请参阅[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)。

2. 启动的 WinDbg 或 KD 的主机计算机上，好像要调试的目标计算机，但不是实际会中断到目标计算机。 若要使用 WinDbg，请使用以下语法。

   **windbg \[-y** <em>KernelSymbolPath</em>**\] \[-k** <em>ConnectionOptions</em>**\]**

   有关此步骤的详细信息，请参阅[Live 内核模式调试使用 WinDbg](performing-kernel-mode-debugging-using-windbg.md)。

   **请注意**作为内核调试程序使用 WinDbg，如果许多 WinDbg 的常见功能将不可用在此方案中。 例如，无法使用局部变量窗口、 反汇编窗口中或调用堆栈窗口中，并且不能单步执行源代码。 这是因为 WinDbg 仅作为调试器 （NTSD 或 CDB） 的查看者在目标计算机上运行。

     

3. 如果没有设置用户模式下的符号路径，则将其设置于输入&gt;提示符。 如果没有设置内核模式符号路径，则将其设置从 kd&gt;提示符。 有关如何访问这些提示以及模式之间切换的信息，请参阅[切换模式](switching-modes.md)。

如果使用 CDB，CDB 与关联的命令提示符窗口保持锁定状态并且不可用而调试将继续进行。 如果使用 NTSD，被创建没有其他窗口，即使 NTSD 具有与之关联的目标计算机上的进程 ID。

如果你想要从用户模式下的调试器运行内核调试程序时还将其用作调试服务器，请参阅[结合使用远程调试的此方法](combining-this-method-with-remote-debugging.md)。

 

 





