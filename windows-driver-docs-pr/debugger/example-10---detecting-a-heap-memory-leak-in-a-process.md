---
title: 示例10检测进程中的堆内存泄漏
description: 示例10检测进程中的堆内存泄漏
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08bae635825a96817e7522c0b518838b01215bd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840839"
---
# <a name="example-10-detecting-a-heap-memory-leak-in-a-process"></a>示例10：检测进程中的堆内存泄漏


## <span id="ddk_example_10___detecting_a_heap_memory_leak_in_a_process_dtools"></span><span id="DDK_EXAMPLE_10___DETECTING_A_HEAP_MEMORY_LEAK_IN_A_PROCESS_DTOOLS"></span>


此示例使用 GFlags 和用户模式转储堆 (UMDH，umdh.exe) ，它是 Windows 调试工具中包含的工具。

**检测中堆内存的泄漏 notepad.exe**

1.  为 notepad.exe 映像文件设置 " [创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md) (**Ust** ") 标志。

    下面的命令使用 GFlags 设置 " **创建用户模式堆栈跟踪数据库** " 标志。 它使用 **/i** 参数来标识图像文件以及标志的 **ust** 缩写。

    ```console
    gflags /i Notepad.exe +ust 
    ```

    作为此命令的结果，将为记事本进程的所有新实例创建用户模式堆栈跟踪。

2.  设置符号文件路径。

    以下命令将创建一个用于存储符号文件目录的路径的环境变量：

    ```console
    set _NT_SYMBOL_PATH=C:\Windows\symbols
    ```

3.  启动记事本。

4.  查找记事本进程 (PID) 的进程标识符。

    可以从任务管理器或 Tasklist ( # A0) （Windows XP Professional 和 Windows Server 2003 操作系统中包含的工具）查找任何正在运行的进程的 PID。 在此示例中，记事本 PID 为1228。

5.  运行 UMDH。

    以下命令运行 UMDH ( # A0) 。 它使用 **-p：** 参数来指定 PID，在本例中为1228。 它使用 **/f：** 参数来指定堆转储、notepad.exe 的输出文件的名称和位置。

    ```console
    umdh -p:1228 -f:notepad.dmp 
    ```

    作为响应，UMDH 将所有活动堆的完整转储写入到 notepad.exe 文件中。

 

 





