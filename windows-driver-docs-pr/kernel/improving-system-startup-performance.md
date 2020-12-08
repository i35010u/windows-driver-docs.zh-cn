---
title: 改进系统启动性能
description: 改进系统启动性能
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e678c577b311f2daa559b430ee4188221334698c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788643"
---
# <a name="improving-system-startup-performance"></a>改进系统启动性能


计算机用户最常请求的功能之一是从关机、待机和休眠状态快速启动时间。 为了缩短启动时间，Windows 将使用多种技术，其中包括：

-   从启动操作列表、进程和服务（可推迟到启动完成后）中删除。

-   根据请求模式预提取内存页，以便在以前的系统启动中加载这些页。

-   将设备初始化与加载操作系统所需的磁盘 i/o 操作重叠。

-   允许并行执行设备初始化，而不是按顺序执行。

内核模式驱动程序应采取以下步骤来提高启动过程的性能：

-   当计算机从电源关闭状态启动 (冷启动) 时，设备驱动程序应该只执行初始化设备所需的操作，并将所有其他设备操作推迟到启动完成。 将驱动程序的初始化代码限制为使设备可以使用所需的操作。

-   当计算机从待机或休眠状态启动 (热启动) 时，必须在启动完成之前初始化的驱动程序应使用高优先级工作线程和关键队列工作项来卸载所需的任何小任务。 否则，驱动程序线程可能会被不相关的线程会耗尽处理器时间，并且启动将会延迟。

-   在从待机或休眠状态进行热启动期间，驱动程序的 DPC 例程或在调度级别运行的初始化代码 \_ 应避免阻止其他驱动程序运行的长时间执行时间。 有关详细信息，请参阅 [在启动过程中从 Low-Power 状态共享处理器资源](sharing-processor-resources-during-startup-from-a-low-power-state.md)。

-   在从待机或休眠状态进行热启动期间，功能设备驱动程序会立即完成 S0 集电源 IRP，然后请求 D0 集电源 IRP。 如果你的驱动程序立即完成 S0 集电源 IRP，则操作系统可以在你的驱动程序将设备重新初始化为后台任务时完成启动。 有关详细信息，请参阅 [快速启动 Low-Power 状态](fast-startup-from-a-low-power-state.md)。

-   设备驱动程序不应将旋转锁定保留一小段时间，尤其是在冷启动时，在电源关闭状态。 否则，其他设备初始化不能并行出现。

本节包括下列主题：

[在从低功耗状态启动期间共享处理器资源](sharing-processor-resources-during-startup-from-a-low-power-state.md)

[从低功耗状态快速启动](fast-startup-from-a-low-power-state.md)

 

 




