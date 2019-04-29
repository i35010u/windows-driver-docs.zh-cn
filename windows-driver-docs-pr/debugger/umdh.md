---
title: 用户模式转储堆 (UMDH) 工具
description: 用户模式转储堆 (UMDH) 工具，Umdh.exe，分析给定进程的 Microsoft Windows 堆内存分配
ms.assetid: 112795a9-57c0-43a4-9f21-2a8655b65d1b
keywords: UMDH，用户模式转储堆
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d54bcb0358effd3bcc743a4102f988d60008d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380773"
---
# <a name="umdh"></a>UMDH


## <span id="ddk_umdh_dtools"></span><span id="DDK_UMDH_DTOOLS"></span>


用户模式转储堆 (UMDH) 工具，Umdh.exe，分析给定进程的 Microsoft Windows 堆内存分配。 UMDH 具有以下模式。

-   **分析正在运行的进程**("模式 1")。 UMDH 捕获和分析进程的堆内存分配。 对于每个分配 UMDH 分配数据和分配堆栈显示分配的大小、 的开销大小、 指针。 如果某个进程拥有多个活动内存堆，UMDH 捕获所有堆。 此分析可以显示实时或保存的日志文件中。

-   **分析日志文件，UMDH** ("模式 2")。 UMDH 分析具有以前创建的日志文件。 UMDH 可以比较两个日志创建相同处理在不同的时间，并且显示调用中分配的大小增加最多了。 此方法可用于查找内存泄漏。

本部分包括：

[准备使用 UMDH](preparing-to-use-umdh.md)

[UMDH 命令](umdh-commands.md)

[解释 UMDH 日志](interpreting-a-umdh-log.md)

[解释日志比较](interpreting-a-log-comparison.md)

 

 





