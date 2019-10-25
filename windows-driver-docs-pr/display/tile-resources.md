---
title: 平铺资源
description: 对于磁贴资源，设备分页队列上运行的异步视频内存管理器服务是不够的。
ms.assetid: D48D2046-64A6-4B0E-9235-84DD2A83DB39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dafc558d169666d2bdec0903a874af3e06f0d37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825497"
---
# <a name="tile-resources"></a>平铺资源


对于磁贴资源，设备分页队列上运行的异步视频内存管理器服务是不够的。 具体而言，对于磁贴资源，我们想要将页表更新与呈现一起排队，并确保在绘图操作之间同步应用更新。

例如，给定应用程序的以下 API 调用顺序：

1.  绘制 \#42
2.  更新磁贴映射
3.  绘制 \#43

我们想要确保*绘图 \#42*在页表处于旧状态的情况下执行，同时*绘制 \#43*在其新状态下以页表的方式执行。 对于指定无覆盖标志的*更新磁贴映射*操作，此同步可能有点宽松，但必须支持高性能同步更新。
为了支持高性能的排队更新，我们需要提前生成分页操作并将它们排队到上下文中，并在依赖呈现上下文达到某个点后等待其执行（例如：在绘图 \#42上文）。

这意味着分页操作需要在图形处理单元（GPU）等待后排队，等待时间由特定的呈现上下文发出信号。 因此，它们无法直接排队到共享系统上下文中，因为这意味着一个应用程序可能会阻止对系统中的其他所有人执行分页操作。

从理论上讲，在今天的基于数据包的计划中，我们可以在设备分页队列中实现操作的等待部分，监视等待，并在满足等待条件后将分页操作提交给共享系统上下文。 但是，当我们在基于数据包的计划之外转移和硬件计划时，我们想要确保可以将 GPU 用于联锁操作的 GPU 同步基元，以确保最佳性能。

若要解决此问题，我们将介绍每个上下文的分页伴随上下文的概念。 在首次调用[*UpdateGpuVirtualAddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)时，会延迟创建分页辅助上下文，并将其用于所有需要联锁同步的页面表更新。 *UpdateGpuVirtualAddress*使用 GPU 监视的防护对象和特定的防护值作为参数。 伴生上下文会等待此监视的隔离，并对页面表进行更新，并增加监视的隔离对象的信号。 这允许呈现上下文与伴生上下文紧密同步。

下面说明了使用伴生上下文的页表更新。

![联锁页表更新](images/tile-resources.1.png)

伴生上下文由视频内存管理器根据内核模式驱动程序在上下文创建期间选择的引擎（**DXGKARG\_CREATECONTEXT）延迟创建。PagingCompanionNodeId**）。

伴生上下文在每个进程的特权地址空间中执行。 地址空间是有特权的，因为它是由内核控制的，并且只允许在内部执行内核中生成的直接内存访问（DMA）缓冲区。 在这种情况下，这是一个正常的 GPU 虚拟地址空间，不需要任何特殊硬件虚拟地址空间权限支持。

出于简单起见，我们选择了每个进程的特权 GPU 虚拟地址空间，而不是重新使用系统分页处理 GPU 虚拟地址空间。 考虑到磁贴资源的映射和取消映射很常见，我们需要将应用程序页表永久映射到地址空间，以避免频繁地映射/取消映射。 此外，正如我们稍后将详细介绍的那样，我们还需要以永久性方式自行映射所有磁贴池。 在系统地址空间中执行这些永久映射会引入不必要的额外复杂性。

将对每个进程的特权 GPU 虚拟地址空间进行初始化，以便在地址空间中可以看到进程 GPU 页表，通过该地址空间，update 命令可以使用 GPU 更新各种页面表项。 此外，进程创建的所有磁贴池还会映射到地址空间。

伴生上下文更新页面表条目的方式有点特殊，需要一些说明。 当*映射*操作排队等待共享系统上下文中执行时，视频内存管理器将知道要映射到的物理地址，并且这些物理地址可以直接显示在关联的分页缓冲区中。 在这种情况下，使用[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作，视频内存管理器保证在某些特定页面上执行分页操作之前，将这些页面重新用于其他目的。

但是，对于伴生上下文中页表的同步更新，这种情况会更加困难。 视频内存管理器知道在生成更新操作时所引用的磁贴池的物理页，但是，如果这些操作将在任意长 GPU 等待时间（应用甚至可能会死锁和永不信号）后排队，视频内存管理器不知道在分页操作实际执行时，平铺池的物理页是什么，视频内存管理器不能在该位置将磁贴池保留任意长的时间。

若要解决此问题，我们实际上需要对分页操作进行排队，并在以后将其修补为物理地址更改，或者需要后期绑定更新中使用的实际地址，视频内存管理器会执行后者。

若要解决此问题，视频内存管理器会执行两个任务。 首先，它将 GPU 虚拟地址映射到进程特权地址空间内属于进程的所有磁贴池元素。 当磁贴池在内存中移动时，视频内存管理器将使用与任何其他分配类型相同的简单机制自动将这些 GPU 虚拟地址指向磁贴池的正确位置。

若要更新磁贴资源页表项，视频内存管理器会引入一个新的**CopyPageTableEntry**分页操作，该操作将页表项从磁贴池虚拟地址复制到磁贴资源虚拟地址。 因为当磁贴池在内存中移动时，视频内存管理器会使磁贴池虚拟地址保持最新状态，因此，无论在多长时间内已生成命令以及实际执行的命令。

请注意，只要有引用特定磁贴池的排队页面表更新，无论用户模式驱动程序或应用程序所说的用户模式驱动程序或应用程序是什么，视频内存管理器就会将该磁贴池保留在驻留要求中，以确保执行更新操作时，磁贴池虚拟地址有效。

此机制如下所示：

![复制页表操作](images/tile-resources.2.png)**

## <a name="span-id_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_modespanspan-id_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_modespanspan-id_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_modespan-update-gpu-virtual-address-on-gpus-with-cpu_virtual-page-table-update-mode"></a><span id="_Update_GPU_virtual_address_on_GPUs_with_CPU_VIRTUAL_page_table_update_mode"></span><span id="_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_mode"></span><span id="_UPDATE_GPU_VIRTUAL_ADDRESS_ON_GPUS_WITH_CPU_VIRTUAL_PAGE_TABLE_UPDATE_MODE"></span>用 CPU\_虚拟页面表更新模式来更新 Gpu 上的 GPU 虚拟地址


在支持**DXGK\_PAGETABLEUPDATE\_CPU\_虚拟**页表更新模式的 gpu 上，不会使用**CopyPageTableEntries**操作。 这些是集成的 GPU，不使用分页缓冲区。 在正确的时间之前，视频内存管理器会将更新操作延迟，并使用[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作来设置页表。

此方法的缺点是[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作不与呈现操作并行。 优点在于，驱动程序无需实现对分页缓冲区的支持并实现*UpdatePageTable*作为即时操作。

 

 





