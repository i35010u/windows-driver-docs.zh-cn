---
title: 平铺资源
description: 有关磁贴资源，运行设备分页队列上的异步视频内存管理器服务不足够。
ms.assetid: D48D2046-64A6-4B0E-9235-84DD2A83DB39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a663c211d154411e5191072aaf1464ca93f3b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389851"
---
# <a name="tile-resources"></a>平铺资源


有关磁贴资源，运行设备分页队列上的异步视频内存管理器服务不足够。 具体而言，磁贴资源我们想要对队列以及呈现的页表更新，确保之间绘制操作以同步方式应用更新。

例如，给定以下 API 调用序列应用程序：

1.  绘制\#42
2.  更新磁贴映射
3.  绘制\#43

我们希望确保*绘制\#42*使用中时其旧状态的页表执行*绘制\#43*使用在其新状态的页表执行。 有关*更新磁贴映射*指定 no-overwrite 标志的操作，此同步可以放宽一点，但必须支持高性能同步更新。
为了支持高性能排队更新，我们需要生成提前分页操作和它们排队到上下文并等待这些依赖呈现上下文达到特定的时间点后要执行的功能 (例如： 绘图后\#42 更高版本)。

这意味着需要背后的图形处理单元 (GPU) 将通过特定呈现上下文来发出信号的等待排入队列的分页操作。 正因为如此，它们不能将排队直接与共享的系统上下文作为这意味着，一个应用程序可能会阻止执行的系统中的其他所有人都分页操作。

从理论上讲，今天的数据包中基于计划我们可以实现设备分页队列中等待部分的操作、 监视等待并等待条件满足后提交到共享的系统上下文的分页操作。 但是，随着我们超出数据包基于计划，然后拖动到我们想要确保我们可以使用 GPU 的 GPU 硬件计划同步基元以供互锁操作以确保最佳性能。

若要解决此问题，我们将引入每个上下文分页随附上下文的概念。 分页随附上下文惰式创建在首次调用[ *UpdateGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906365)和用于需要互锁的同步的所有页表更新。 *UpdateGpuVirtualAddress*将监视的 GPU fence 对象和特定限制值作为参数。 随附上下文等待对此受监视的 fence 页表更新然后递增监视的 fence 对象并向它发出信号。 这允许呈现上下文与配套上下文紧密同步。

使用随附的上下文的页表更新如下图所示。

![互锁的页表更新](images/tile-resources.1.png)

随附上下文惰式创建上下文创建期间选择的内核模式驱动程序的引擎针对视频内存管理器 (**DXGKARG\_CREATECONTEXT。PagingCompanionNodeId**)。

在每个进程特权的地址空间中执行随附上下文。 因为它是同时由内核控制，允许仅在内核中生成的直接内存访问 (DMA) 缓冲区内执行的地址空间是一项特权。 外部的这是正常的 GPU 虚拟地址空间，不需要任何特殊硬件的虚拟地址空间特权支持。

我们选择每个进程特权 GPU 虚拟地址空间，而不是重新使用系统分页进程 GPU 虚拟地址空间为简单起见。 假设映射和取消映射磁贴的资源很常见，我们需要应用程序页表中的地址空间可以避免不得不映射/取消映射这些经常永久映射。 此外，如我们稍后将详细介绍，我们需要映射的所有磁贴池本身以永久方式。 这些永久系统地址空间中的映射将引入不必要的其他复杂性。

从而使进程 GPU 页表都通过使得更新命令来更新使用 GPU 的各页表项的地址空间可见初始化每个进程特权的 GPU 虚拟地址空间。 此外，由进程创建的池也将映射到的地址空间的所有磁贴。

页表项更新随附上下文的方法是有点特殊，需要一些说明。 当*映射*操作排队等待执行共享的系统上下文、 视频内存管理器知道要映射到的物理地址和这些物理地址可以直接在关联的分页缓冲区中出现。 [*UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)这种情况下使用分页操作和视频内存管理器可保证在一些特定的页上的分页操作将完成之前这些页重新用于其他用途。

但是，对于页面上的表的配套上下文的同步更新，情况会更加困难。 视频内存管理器知道物理页的磁贴池正在引用时生成的 update 操作，但是，给定的这些操作将排队等候，后面任意长 GPU 等待 （应用程序可能甚至发生死锁和永远不会发出信号），视频内存管理器不知道在实际执行操作执行分页操作时，磁贴池的物理页将是什么，视频内存管理器不能保持该磁贴池在该位置的任意长的时间。

若要解决此问题，我们实质上是需要分页操作进行排队并稍后根据物理地址更改，或者我们需要后期绑定的更新中使用的实际地址修补，视频内存管理器，会执行后一种。

若要解决此问题的视频内存管理器，请执行两项操作。 首先，它将 GPU 虚拟地址映射到的所有磁贴池元素属于某个进程的特权的进程地址空间内。 当在内存中移动磁贴池时，视频内存管理器自动会保留指向正确的位置使用相同的简单机制的任何其他分配类型的磁贴池这些 GPU 虚拟地址。

若要更新磁贴资源页表项，视频内存管理器引入了新**CopyPageTableEntry**分页操作，它将从磁贴池虚拟地址的页表项复制到的磁贴资源虚拟地址。 因为视频内存管理器中保存的磁贴池虚拟地址最新的磁贴池移动在内存中，复制操作可确保无论多少时间之间的磁贴池的当前有效的物理位置执行具有生成的命令和实际执行的命令。

请注意，只要有引用特定平铺池排队的页表更新，视频内存管理器将在用户模式驱动程序或应用程序说，以保证，无论应用程序的驻留要求保留该磁贴池当执行更新操作时，磁贴池虚拟地址都有效。

此机制如下图所示：

![复制页面表操作](images/tile-resources.2.png)**

## <a name="span-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespanspan-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespanspan-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespan-update-gpu-virtual-address-on-gpus-with-cpuvirtual-page-table-update-mode"></a><span id="_Update_GPU_virtual_address_on_GPUs_with_CPU_VIRTUAL_page_table_update_mode"></span><span id="_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_mode"></span><span id="_UPDATE_GPU_VIRTUAL_ADDRESS_ON_GPUS_WITH_CPU_VIRTUAL_PAGE_TABLE_UPDATE_MODE"></span> CPU 使用更新的 Gpu 上的 GPU 虚拟地址\_虚拟页表更新模式


在 Gpu 上的支持**DXGK\_PAGETABLEUPDATE\_CPU\_虚拟**页表更新模式下**CopyPageTableEntries**操作不会使用。 这些集成 GPU，不要使用分页缓冲区。 视频内存管理器将推迟到适当的时间和使用更新操作[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)操作设置页上的表。

此方法的缺点在于[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)均不与呈现操作的并行操作。 优点是，该驱动程序不需要实现对分页缓冲区的支持和实施*UpdatePageTable*作为一项即时操作。

 

 





