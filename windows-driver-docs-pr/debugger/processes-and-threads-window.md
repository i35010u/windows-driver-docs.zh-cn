---
title: 在 WinDbg 中控制进程和线程
description: 在 WinDbg 中控制进程和线程
keywords:
- "\"调试信息\" 窗口、\"进程\" 和 \"线程\" 窗口"
- "\"进程和线程\" 窗口"
- "\"进程\"、\"进程\" 和 \"线程\" 窗口"
- "\"线程、进程和线程\" 窗口"
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 636fb4b8f208e34a2a77fc08b1168d133ff0717d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840829"
---
# <a name="controlling-processes-and-threads-in-windbg"></a>在 WinDbg 中控制进程和线程


## <span id="ddk_processes_and_threads_window_dbg"></span><span id="DDK_PROCESSES_AND_THREADS_WINDOW_DBG"></span>


在 WinDbg 中，"进程" 和 "线程" 窗口显示有关正在调试的系统、进程和线程的信息。 此窗口还允许您选择要激活的新系统、进程和线程。

### <a name="span-idopening_the_processes_and_threads_windowspanspan-idopening_the_processes_and_threads_windowspanopening-the-processes-and-threads-window"></a><span id="opening_the_processes_and_threads_window"></span><span id="OPENING_THE_PROCESSES_AND_THREADS_WINDOW"></span>打开 "进程和线程" 窗口

若要打开 "进程和线程" 窗口，请从 "**视图**" 菜单中选择 "**进程和线程**"。  (还可以按 ALT + 9，或在工具栏上的 "进程和线程") 按钮 (屏幕截图中选择 " **进程和线程** " 按钮 ![ ](images/window-processes-threads.png) 。 ALT + SHIFT + 9 关闭 "进程和线程" 窗口。 ) 

下面的屏幕截图显示了 "进程" 和 "线程" 窗口的示例。

!["进程和线程" 窗口的屏幕截图](images/window-prth.png)

"进程" 和 "线程" 窗口显示当前正在调试的所有进程的列表。 进程中的线程显示在每个进程下。 如果将调试器附加到多个系统，则系统会显示在树的顶层，其中包含这些系统的进程，以及从属于进程的线程。

每个系统列表包括服务器名称和协议详细信息。 运行调试器的系统标识为 " **&lt; 本地 &gt;**"。

每个进程列表都包含调试器使用的内部十进制进程索引、十六进制进程 ID 以及与进程关联的应用程序的名称。

每个线程列表都包含调试器使用的内部十进制线程索引和十六进制线程 ID。

### <a name="span-idusing_the_processes_and_threads_windowspanspan-idusing_the_processes_and_threads_windowspanusing-the-processes-and-threads-window"></a><span id="using_the_processes_and_threads_window"></span><span id="USING_THE_PROCESSES_AND_THREADS_WINDOW"></span>使用 "进程和线程" 窗口

在 "进程" 和 "线程" 窗口中，当前或活动的系统、进程和线程以粗体显示。 若要使新的系统、进程或线程处于活动状态，请在窗口中选择其行。

"进程" 和 "线程" 窗口具有包含附加命令的快捷菜单。 若要访问菜单，请选择并按住 (或右键单击标题栏) ，或选择窗口右上角附近的图标 (![显示 "暂存板" 窗口工具栏快捷菜单的按钮屏幕截图](images/window-processes-threads.png)). 以下列表描述了一些菜单命令：

-   **移动到新的停靠** 将关闭 "进程和线程" 窗口，并在新的停靠中打开它。

-   **始终浮动** 会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   "**移动到帧**" 会导致在移动 WinDbg 帧时窗口移动，即使窗口未停靠也是如此。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关显示或控制系统的其他方法，请参阅 [调试多个目标](debugging-multiple-targets.md)。 有关显示或控制进程和线程的其他方法，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

 

 





