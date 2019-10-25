---
title: 在从低功耗状态启动期间共享处理器资源
description: 在从低功耗状态启动期间共享处理器资源
ms.assetid: 2b2e6a1b-7c2d-4f38-9407-a417b75daa6a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e7e600b3d838de7aee2663134c640a1952d57526
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838422"
---
# <a name="sharing-processor-resources-during-startup-from-a-low-power-state"></a>在从低功耗状态启动期间共享处理器资源


从待机或休眠状态（热启动）启动计算机时，驱动程序应避免使用比所需时间更长的处理器资源。 最重要的是，延迟的过程调用（DPC）例程和执行代码（以 IRQL &gt;= 调度\_级别的代码）应将其执行时间保持在最小值。 驱动程序使用 DPC 例程来帮助初始化设备。 驱动程序可能需要作为端口微型端口接口协定的一部分，在调度\_级别运行初始化代码。

当 DPC 例程运行时，将阻止在同一处理器上运行较低优先级的其他线程。 此外，在当前 DPC 完成之前，已排队并准备运行的其他 DPC 例程可能会被阻止。 为了使其他线程能够运行 expediently，典型的 DPC 例程运行不超过100毫秒。

在系统启动期间运行时间太长的 DPC 例程可能会延迟其他设备的初始化。 这种延迟会使设备初始化阶段更长时间，并使操作系统延迟启动完成。

使用以下最佳实践设计 DPC 例程：

-   单个 DPC 例程的执行不应超过100毫秒。

-   调用[**KeStallExecutionProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)例程以延迟执行的 DPC 例程不得指定超过100毫秒的延迟。

-   如果任务需要超过100微秒并在调度\_级别执行，则 DPC 例程应在100微秒后结束，并计划一个或多个 DPC 计时器例程以便以后完成该任务。

-   使用 WDK 中记录的性能分析工具来评估 DPC 例程的执行时间。

有关性能分析工具的详细信息，请参阅[在 Windows Vista 上测量系统恢复性能](https://go.microsoft.com/fwlink/p/?linkid=69964)。

 

 




