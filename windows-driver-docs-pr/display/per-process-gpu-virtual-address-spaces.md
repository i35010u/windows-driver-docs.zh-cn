---
title: 每个进程的 GPU 虚拟地址空间
description: 每个进程都具有两个图形处理单元 (GPU) 虚拟地址空间、 应用程序 GPU 虚拟地址空间和特权的虚拟地址空间相关联。
ms.assetid: 6C7BF67B-217D-4E21-B425-5683C99B63A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 485726cc6508ff252961df86f4b3a44ef3f48d9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352289"
---
# <a name="span-iddisplayper-processgpuvirtualaddressspacesspanper-process-gpu-virtual-address-spaces"></a><span id="display.per-process_gpu_virtual_address_spaces"></span>每个进程的 GPU 虚拟地址空间


每个进程都具有两个图形处理单元 (GPU) 虚拟地址空间、 应用程序 GPU 虚拟地址空间和特权的虚拟地址空间相关联。

## <a name="span-idapplicationgpuvirtualaddressspacespanspan-idapplicationgpuvirtualaddressspacespanspan-idapplicationgpuvirtualaddressspacespanapplication-gpu-virtual-address-space"></a><span id="Application_GPU_virtual_address_space"></span><span id="application_gpu_virtual_address_space"></span><span id="APPLICATION_GPU_VIRTUAL_ADDRESS_SPACE"></span>应用程序 GPU 虚拟地址空间


应用程序 GPU 虚拟地址空间是在中执行的命令缓冲区，生成的用户模式驱动程序的地址空间。 此地址空间由使用提供的视频内存管理器服务的用户模式驱动程序管理。 在虚拟模式下运行的 GPU 引擎时可以访问分配之前，用户模式驱动程序必须将 GPU 虚拟地址范围分配给分配。 对于常规的分配，这是使用新[ *MapGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906358)视频内存管理器公开的服务。 *MapGpuVirtualAddress*允许到任一选取用户模式驱动程序特定的地址，其中它想要映射的分配或可自动选择可用的 GPU 虚拟地址的视频内存管理器使用它。 驱动程序通常应让视频内存管理器会自动选取的地址，但在某些情况下，驱动程序可能需要更多控制。 在链接的显示适配器配置中， *MapGpuVirtualAddress*还可用于指定映射是当前在 GPU 上或对等方 GPU 上的分配的实例。 *MapGpuVirtualAddress*到视频内存管理器请求进行排队并立即时处理该请求返回给用户模式驱动程序。 在设备分页队列中排队请求和用户模式驱动程序必须确保它针对分页围栏值返回设备同步。 [*FreeGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906356)可用于取消映射分配和回收其 GPU 虚拟地址。 分配被销毁，因此用户模式驱动程序不需要显式取消映射时自动释放所有关联的分配的虚拟地址。 视频内存管理器提供了两个磁贴对用户模式驱动程序的特定于资源的服务。 [*ReserveGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906359)允许用户模式驱动程序，以保留磁贴资源的地址空间和[ *UpdateGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906365)允许用户模式驱动程序映射和取消映射到特定磁贴池页面磁贴资源所在区域。 *ReserveGpuVirtualAddress*执行针对设备分页队列，而*UpdateGpuVirtualAddress*运行进程的特权的地址空间内的特殊随附上下文中执行。

## <a name="span-idprocessprivilegedvirtualaddressspacespanspan-idprocessprivilegedvirtualaddressspacespanspan-idprocessprivilegedvirtualaddressspacespanprocess-privileged-virtual-address-space"></a><span id="Process_privileged_virtual_address_space"></span><span id="process_privileged_virtual_address_space"></span><span id="PROCESS_PRIVILEGED_VIRTUAL_ADDRESS_SPACE"></span>进程的特权虚拟地址空间


使用磁贴资源的进程将获取在第一个调用与之关联的第二个虚拟地址空间[ *ReserveGpuVirtualAddress*](https://msdn.microsoft.com/library/windows/hardware/dn906359)。 此地址空间用于以同步方式更新过程的页表中的呈现。 我们将介绍在此地址空间[磁贴资源](tile-resources.md)主题。

## <a name="span-idvirtualaddressspaceonlinkeddisplayadaptersspanspan-idvirtualaddressspaceonlinkeddisplayadaptersspanspan-idvirtualaddressspaceonlinkeddisplayadaptersspanvirtual-address-space-on-linked-display-adapters"></a><span id="Virtual_address_space_on_linked_display_adapters"></span><span id="virtual_address_space_on_linked_display_adapters"></span><span id="VIRTUAL_ADDRESS_SPACE_ON_LINKED_DISPLAY_ADAPTERS"></span>链接的显示适配器上的虚拟地址空间


链接物理图形适配器时链接到显示适配器链，就仍有单个 GPU 虚拟地址空间，每个进程 （除分页过程中）。 但每个物理适配器上的虚拟地址空间映射由其自己的页表集。

 

 





