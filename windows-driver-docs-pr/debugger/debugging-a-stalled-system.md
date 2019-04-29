---
title: 调试已停止的系统
description: 调试已停止的系统
ms.assetid: 83679dca-2477-4d03-9a89-5a5aebc7b9d9
keywords:
- 停止的系统调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187712a6006aef96a60e99ff97d5469a07d2f08d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324590"
---
# <a name="debugging-a-stalled-system"></a>调试已停止的系统


## <span id="ddk_debugging_a_stalled_system_dbg"></span><span id="DDK_DEBUGGING_A_STALLED_SYSTEM_DBG"></span>


有些的时候计算机时停止响应，而不实际启动的 bug 检查。 此"冻结"可以出现在各种形式：

-   鼠标指针可以移动，但不会影响任何 windows 在屏幕上。

-   整个屏幕仍和鼠标指针不会移动，但分页的内存和磁盘之间将继续。

-   仍然是屏幕，并且该磁盘是无提示。

如果鼠标指针移动，或者没有分页到磁盘，这通常是由于客户端服务器运行时子系统 (CSRSS) 中的问题。

如果 NTSD CSRSS 上运行，请按 F12，每个线程，转储以查看是否有任何特别之处。 (请参阅[调试 CSRSS](debugging-csrss.md)的更多详细信息。)

如果 CSRSS 检查显示执行任何操作，则问题可能是与内核别忘了。

如果没有鼠标移动或分页，则几乎可以肯定内核问题。

分析此类内核崩溃通常是一个困难的任务。 若要开始，分解成 KD (与[ **CTRL + C**](ctrl-c--break-.md)) 或 WinDbg (与**CTRL + BREAK**)。 现在可以使用调试器命令以检查这种情况。

在此事例包含一些有用的技术：

[查找失败的进程](finding-the-failed-process.md)

[调试中断 Storm](debugging-an-interrupt-storm.md)

 

 





