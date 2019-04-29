---
title: 改进系统启动性能
description: 改进系统启动性能
ms.assetid: 9fce451c-73b3-4e3b-875d-319aaa8765ff
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f96db85ed44e261d2a66f23b92881db216a296a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384257"
---
# <a name="improving-system-startup-performance"></a>改进系统启动性能


计算机用户最常请求的功能之一是从关闭电源、 standby 和休眠状态的快速启动时间。 若要减少启动时间，Windows 使用多种方法，包括以下各项：

-   从列表中删除的启动操作、 进程和服务的启动完成后可以推迟至。

-   预提取的请求加载这些页中上一系统初创企业模式的内存页。

-   重叠设备初始化与加载操作系统所需的磁盘 I/O 操作。

-   启用设备初始化并行而不是按顺序执行。

内核模式驱动程序应执行以下步骤以提高启动过程的性能：

-   在计算机启动时从关闭电源状态 （冷启动），设备驱动程序应该做什么，才需要初始化设备并启动完成之前将所有其他设备操作的延迟。 限制您的驱动程序的初始化代码，使设备准备好使用所需的操作。

-   在计算机启动时从待机或休眠状态 （热启动），启动完成之前必须初始化的驱动程序应使用高优先级工作线程和关键队列工作项卸载它要求任何小任务。 否则为可能由不相关线程的处理器时间百分比缺少驱动程序线程，启动将被延迟。

-   在从待机或休眠状态的热启动时，驱动程序的 DPC 例程或初始化代码，在运行调度\_级别，应避免长时间阻止运行其他驱动程序的执行时间。 有关详细信息，请参阅[共享处理器资源期间启动从低功耗状态](sharing-processor-resources-during-startup-from-a-low-power-state.md)。

-   热启动期间从待机或休眠状态，功能的设备驱动程序应立即完成 S0 集 power IRP，然后请求 D0 集 power IRP。 如果您的驱动程序立即完成 S0 集 power IRP，操作系统可以完成启动，同时您的驱动程序重新初始化将设备作为后台任务。 有关详细信息，请参阅[快速启动从低功耗状态](fast-startup-from-a-low-power-state.md)。

-   设备驱动程序不应阻止很短的时间，尤其是在关闭电源状态从冷启动期间超过的自旋锁。 否则，其他设备初始化不能会并行发生。

本部分包括以下主题：

[在从低功耗状态启动期间共享处理器资源](sharing-processor-resources-during-startup-from-a-low-power-state.md)

[从低功耗状态的快速启动](fast-startup-from-a-low-power-state.md)

 

 




