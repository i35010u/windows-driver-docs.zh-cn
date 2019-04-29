---
title: 在 WinDbg 中控制进程和线程
description: 在 WinDbg 中控制进程和线程
ms.assetid: d4755889-9a65-4e81-b3a3-e0bbc6324d3e
keywords:
- 调试信息窗口、 进程和线程窗口
- 进程和线程窗口
- 进程、 进程和线程窗口
- 线程、 进程和线程窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee0b3de8d15f9fa23b2c7c754efbcf7716f5e14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362406"
---
# <a name="controlling-processes-and-threads-in-windbg"></a>在 WinDbg 中控制进程和线程


## <span id="ddk_processes_and_threads_window_dbg"></span><span id="DDK_PROCESSES_AND_THREADS_WINDOW_DBG"></span>


在 WinDbg 中，进程和线程窗口中显示有关系统、 进程和线程正在调试的信息。 此窗口还可选择新的系统、 进程和线程处于活动状态。

### <a name="span-idopeningtheprocessesandthreadswindowspanspan-idopeningtheprocessesandthreadswindowspanopening-the-processes-and-threads-window"></a><span id="opening_the_processes_and_threads_window"></span><span id="OPENING_THE_PROCESSES_AND_THREADS_WINDOW"></span>打开的进程和线程窗口

若要打开进程和线程窗口中，选择**进程和线程**从**视图**菜单。 (还可以按 ALT + 9，或单击**进程和线程**按钮 (![进程和线程按钮的屏幕截图](images/window-processes-threads.png)) 工具栏上。 ALT + SHIFT + 9 关闭进程和线程窗口中。）

以下屏幕截图显示进程和线程窗口的一个示例。

![进程和线程窗口的屏幕截图](images/window-prth.png)

进程和线程窗口中显示的所有当前正在调试的进程的列表。 进程中的线程显示下每个进程。 如果调试器已附加到多个系统，系统会显示在树中，与从属于，进程和从属到的进程线程的最高级别。

每个系统列表包括服务器名称和协议详细信息。 系统上运行调试器都会被视为**&lt;本地&gt;**。

每个进程列表包括调试器使用的内部小数过程索引、 十六进制的进程 ID 和与该进程关联的应用程序的名称。

每个线程列表包括调试器使用的内部小数线程索引和十六进制的线程 id。

### <a name="span-idusingtheprocessesandthreadswindowspanspan-idusingtheprocessesandthreadswindowspanusing-the-processes-and-threads-window"></a><span id="using_the_processes_and_threads_window"></span><span id="USING_THE_PROCESSES_AND_THREADS_WINDOW"></span>使用进程和线程窗口

在进程和线程窗口中，当前或处于活动状态的系统、 进程和线程以粗体显示。 若要使新的系统、 进程或线程处于活动状态，请单击窗口中的一行。

进程和线程窗口具有带其他命令的快捷方式菜单。 若要访问菜单，请右键单击标题栏或单击窗口 （在右上角附近的图标![显示的草稿板窗口工具栏快捷方式菜单按钮的屏幕截图](images/window-processes-threads.png))。 以下列表介绍了一些菜单命令：

-   **移到新停靠**关闭进程和线程窗口中，并将其打开新的平台中。

-   **始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   **移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

显示或控制系统的其他方法，请参阅[调试多个目标](debugging-multiple-targets.md)。 显示或控制进程和线程的其他方法，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

 

 





