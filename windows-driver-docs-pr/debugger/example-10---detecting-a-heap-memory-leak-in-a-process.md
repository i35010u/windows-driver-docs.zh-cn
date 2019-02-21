---
title: 示例 10 检测进程中的堆内存泄漏
description: 示例 10 检测进程中的堆内存泄漏
ms.assetid: ec98dd96-b12b-4f83-85e8-2c5ee32fc17e
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e04334e3cf26dd734a7964d974e62f832f650ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542722"
---
# <a name="example-10-detecting-a-heap-memory-leak-in-a-process"></a>示例 10:在进程中检测堆内存泄漏


## <span id="ddk_example_10___detecting_a_heap_memory_leak_in_a_process_dtools"></span><span id="DDK_EXAMPLE_10___DETECTING_A_HEAP_MEMORY_LEAK_IN_A_PROCESS_DTOOLS"></span>


此示例使用 GFlags 和用户模式转储堆 （UMDH，umdh.exe），在将调试工具 Microsoft 的 Windows 中包含的工具。

**若要在堆的内存中 notepad.exe 检测泄漏**

1.  设置[创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md)(**ust**) notepad.exe 图像文件的标志。

    以下命令使用 GFlags 设置**创建用户模式堆栈跟踪数据库**标志。 它使用 **/i**参数来标识图像文件和**ust**标志的缩写。

    ```console
    gflags /i Notepad.exe +ust 
    ```

    此命令的结果为 Notepad 进程的所有新实例创建用户模式堆栈跟踪。

2.  设置符号文件路径。

    以下命令创建存储的符号文件的目录的路径的环境变量：

    ```console
    set _NT_SYMBOL_PATH=C:\Windows\symbols
    ```

3.  启动记事本。

4.  查找 Notepad 进程的进程标识符 (PID)。

    你可以从任务管理器或任务列表 (tasklist.exe)，Windows XP Professional 和 Windows Server 2003 操作系统中包含的工具来查找任何正在运行的进程的 PID。 在此示例中，记事本 PID 是 1228年。

5.  运行 UMDH。

    以下命令运行 UMDH (umdh.exe)。 它使用 **-p:** 参数来指定，在此示例中，为 1228 PID。 它使用 **/f:** 参数指定的名称和堆转储，输出文件的位置 notepad.dmp。

    ```console
    umdh -p:1228 -f:notepad.dmp 
    ```

    在响应中，UMDH 写入完整的 notepad.dmp 文件的所有活动堆转储。

 

 





