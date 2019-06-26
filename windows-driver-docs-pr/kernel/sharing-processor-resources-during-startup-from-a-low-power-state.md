---
title: 在从低功耗状态启动期间共享处理器资源
description: 在从低功耗状态启动期间共享处理器资源
ms.assetid: 2b2e6a1b-7c2d-4f38-9407-a417b75daa6a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6f6823ec88b22d38a04b8820580ded20d35ddcb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383020"
---
# <a name="sharing-processor-resources-during-startup-from-a-low-power-state"></a>在从低功耗状态启动期间共享处理器资源


当计算机从待机或休眠状态 （热启动） 启动时，驱动程序应避免不必要更长时间使用的处理器资源。 最重要的是，延迟过程调用 (DPC) 例程和代码执行在 IRQL &gt;= 调度\_级别应尽可能地减小其执行时间。 驱动程序使用 DPC 例程以帮助初始化设备。 驱动程序可能需要在调度运行初始化代码\_级别作为端口微型端口接口协定的一部分。

DPC 例程时，会阻止较低优先级的其他线程在同一个处理器上运行。 此外，当前 DPC 完成之前，可能无法进行排队并准备好运行的其他 DPC 例程。 若要启用其他线程来有效地运行，典型的 DPC 例程应运行不超过 100 个微秒为单位。

在系统启动期间太长时间运行的 DPC 例程可能会延迟初始化的其他设备。 此延迟使得由操作系统的设备初始化阶段长度和延迟启动完成。

使用以下最佳实践来设计 DPC 例程：

-   单个 DPC 例程不应执行的多个 100 微秒为单位。

-   DPC 调用的例程[ **KeStallExecutionProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kestallexecutionprocessor)来延迟执行的例程不能指定多个 100 微秒为单位的延迟。

-   如果任务需要超过 100 微秒为单位，并且执行在调度\_级别 DPC 例程应在 100 微秒后结束和计划在以后完成此任务的一个或多个 DPC 计时器例程。

-   使用 WDK 评估 DPC 例程的执行时间中所述的性能分析工具。

有关性能分析工具的详细信息，请参阅[在 Windows Vista 上测量系统恢复性能](https://go.microsoft.com/fwlink/p/?linkid=69964)。

 

 




