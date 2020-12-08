---
title: 启动调试会话
description: 启动调试会话
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14fd1ec729aa25502fe3dca4f8c6b090a9459d1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783435"
---
# <a name="starting-the-debugging-session"></a>启动调试会话


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


在本文档中如何 [控制内核调试器中的用户模式调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)， *目标应用程序* 指的是正在调试的用户模式应用程序， *目标计算机* 指的是包含目标应用程序的计算机和 NTSD 或 CDB 进程，而 *主机计算机* 指的是包含内核调试器的计算机。

若要开始使用此方法，必须执行以下操作。 可以按任意顺序执行步骤1和步骤2。

1. 在目标计算机上启动 NTSD 或 CDB，并提供-d 命令行选项。

   例如，可以使用以下语法附加到正在运行的进程。

   **ntsd-d \[ -y** <em>UserSymbolPath</em> **\] -p** *PID*

   或者，您可以使用以下语法作为目标来启动一个新进程。

   **ntsd-d. \[** <em>UserSymbolPath</em> **\]** *ApplicationName*

   如果要将此安装为事后调试器，请使用以下语法。

   **ntsd-d. \[** <em>UserSymbolPath</em>**\]**

   有关此步骤的详细信息，请参阅 [使用 CDB 调试 User-Mode 进程](debugging-a-user-mode-process-using-cdb.md)。

2. 在主计算机上启动 WinDbg 或 KD，就像打算调试目标计算机一样，但实际上不会中断目标计算机。 若要使用 WinDbg，请使用以下语法。

   **windbg \[ -y** <em>KernelSymbolPath</em> **\] \[ -k** <em>ConnectionOptions</em>**\]**

   有关此步骤的详细信息，请参阅 [使用 WinDbg 进行实时 Kernel-Mode 调试](performing-kernel-mode-debugging-using-windbg.md)。

   **注意**  如果使用 WinDbg 作为内核调试器，则在这种情况下，很多熟悉的 WinDbg 功能都不能使用。 例如，不能使用 "局部变量" 窗口、"反汇编" 窗口或 "调用堆栈" 窗口，也不能单步执行源代码。 这是因为，WinDbg 只充当在目标计算机上运行的调试程序 (NTSD 或 CDB) 的查看器。

     

3. 如果尚未设置用户模式符号路径，请从输入提示进行设置 &gt; 。 如果尚未设置内核模式符号路径，请从 kd &gt; 提示符设置。 有关如何访问这些提示并在模式之间切换的信息，请参阅 [切换模式](switching-modes.md)。

如果使用 CDB，则与 CDB 关联的命令提示符窗口将保持锁定状态，并且在调试继续时不可用。 如果使用 NTSD，则不会创建任何其他窗口，即使 NTSD 在目标计算机上具有与之关联的进程 ID。

如果要从内核调试器运行用户模式调试器，同时同时将其用作调试服务器，请参阅将 [此方法与远程调试结合](combining-this-method-with-remote-debugging.md)使用。

 

 





