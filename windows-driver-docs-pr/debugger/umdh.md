---
title: User-Mode 转储堆 (UMDH) 工具
description: User-Mode 转储堆 (UMDH) 工具 Umdh.exe，用于分析给定进程的 Microsoft Windows 堆内存分配
keywords: UMDH，User-Mode 转储堆
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9d3580e21edd2b06a6bc37ea6da895b921f756
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803251"
---
# <a name="umdh"></a>UMDH


## <span id="ddk_umdh_dtools"></span><span id="DDK_UMDH_DTOOLS"></span>


User-Mode 转储堆 (UMDH) 工具 Umdh.exe，用于分析给定进程的 Microsoft Windows 堆内存分配。 UMDH 具有以下模式。

-   )  ( "模式 1"**分析正在运行的进程**。 UMDH 捕获并分析进程的堆内存分配。 对于每个分配，UMDH 显示分配的大小、开销的大小、指向分配的指针和分配堆栈。 如果进程具有多个活动内存堆，UMDH 将捕获所有堆。 此分析可以实时显示，也可以保存在日志文件中。

-   **分析 UMDH 日志文件** ( "Mode 2" ) 。 UMDH 分析之前创建的日志文件。 UMDH 可以比较在不同时间为同一进程创建的两个日志，并显示分配大小增加最多的调用。 此方法可用于查找内存泄漏。

本节包括：

[准备使用 UMDH](preparing-to-use-umdh.md)

[UMDH 命令](umdh-commands.md)

[解释 UMDH 日志](interpreting-a-umdh-log.md)

[解释日志比较结果](interpreting-a-log-comparison.md)

 

 





