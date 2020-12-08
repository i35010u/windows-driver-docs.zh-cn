---
title: 调试已停止的系统
description: 调试已停止的系统
keywords:
- 停止系统调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1944a685f5c7f5a3da33fd9240b80a82ddbe5177
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792465"
---
# <a name="debugging-a-stalled-system"></a>调试已停止的系统


## <span id="ddk_debugging_a_stalled_system_dbg"></span><span id="DDK_DEBUGGING_A_STALLED_SYSTEM_DBG"></span>


有时，计算机可以停止响应，而无需实际启动 bug 检查。 此 "冻结" 可在各种形式下出现：

-   鼠标指针可以移动，但不会影响屏幕上的任何窗口。

-   整个屏幕仍然不会移动，但会在内存和磁盘之间继续分页。

-   屏幕仍然为，磁盘处于无提示。

如果鼠标指针移动或对磁盘进行分页，这通常是由于客户端服务器中的问题 Run-Time 子系统 (CSRSS) 。

如果 NTSD 在 CSRSS 上运行，请按 F12 并向外转储每个线程，以查看是否有任何问题。 有关更多详细信息，请参阅 [CSRSS 调试](debugging-csrss.md) 。 )  (

如果 CSRSS 的检查不显示任何内容，则问题可能出在内核之后。

如果没有鼠标移动或分页，则几乎可以肯定是内核问题。

分析此类内核崩溃通常是一件很困难的任务。 若要开始，请通过 ctrl [**+ C**](ctrl-c--break-.md)) 或通过 **ctrl + break**)  (中断 KD (。 你现在可以使用调试器命令来检查此情况。

在这种情况下，有一些有用的技巧包括：

[查找失败的进程](finding-the-failed-process.md)

[调试中断风暴](debugging-an-interrupt-storm.md)

 

 





