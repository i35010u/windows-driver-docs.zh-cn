---
title: 每个进程的 GPU 虚拟地址空间
description: 每个进程都与两个图形处理单元相关联 (GPU) 虚拟地址空间、应用程序 GPU 虚拟地址空间和特权虚拟地址空间。
ms.assetid: 6C7BF67B-217D-4E21-B425-5683C99B63A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b032e9b5f8b35e5e62106da1ed8fbc35154d856
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064670"
---
# <a name="span-iddisplayper-process_gpu_virtual_address_spacesspanper-process-gpu-virtual-address-spaces"></a><span id="display.per-process_gpu_virtual_address_spaces"></span>每个进程的 GPU 虚拟地址空间


每个进程都与两个图形处理单元相关联 (GPU) 虚拟地址空间、应用程序 GPU 虚拟地址空间和特权虚拟地址空间。

## <a name="span-idapplication_gpu_virtual_address_spacespanspan-idapplication_gpu_virtual_address_spacespanspan-idapplication_gpu_virtual_address_spacespanapplication-gpu-virtual-address-space"></a><span id="Application_GPU_virtual_address_space"></span><span id="application_gpu_virtual_address_space"></span><span id="APPLICATION_GPU_VIRTUAL_ADDRESS_SPACE"></span>应用程序 GPU 虚拟地址空间


应用程序 GPU 虚拟地址空间是由用户模式驱动程序生成的命令缓冲区的地址空间，在中执行。 此地址空间由用户模式驱动程序使用视频内存管理器提供的服务进行管理。 在虚拟模式下操作的 GPU 引擎可以访问分配之前，用户模式驱动程序必须为分配分配 GPU 虚拟地址范围。 对于常规分配，此操作使用由视频内存管理器公开的新 [*MapGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_mapgpuvirtualaddresscb) 服务来完成。 *MapGpuVirtualAddress* 允许用户模式驱动程序选择要在其中映射分配的特定地址，或允许视频内存管理器自动选取可用的 GPU 虚拟地址。 驱动程序通常会让视频内存管理器自动选取一个地址，但在某些情况下，驱动程序可能需要更多的控制。 在链接的显示适配器配置中，还可以使用 *MapGpuVirtualAddress* 来指定映射是在当前 GPU 上还是对等 GPU 上分配的实例。 *MapGpuVirtualAddress* 将请求排队，并在处理请求时立即返回到用户模式驱动程序。 请求在设备分页队列上排队，用户模式驱动程序必须确保它与返回的设备分页防护值同步。 [*FreeGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_freegpuvirtualaddresscb) 可用于取消分配，并回收其 GPU 虚拟地址。 分配被销毁时，与分配关联的所有虚拟地址都将自动释放，因此用户模式驱动程序无需显式取消映射。 视频内存管理器向用户模式驱动程序提供两个特定于磁贴资源的服务。 [*ReserveGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb) 允许用户模式驱动程序为磁贴资源保留地址空间， [*UpdateGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb) 允许用户模式驱动程序将磁贴资源的区域映射到特定的磁贴池页面。 *ReserveGpuVirtualAddress* 针对设备分页队列执行，而 *UpdateGpuVirtualAddress* 在进程的特权地址空间内运行的特殊伴生上下文中执行。

## <a name="span-idprocess_privileged_virtual_address_spacespanspan-idprocess_privileged_virtual_address_spacespanspan-idprocess_privileged_virtual_address_spacespanprocess-privileged-virtual-address-space"></a><span id="Process_privileged_virtual_address_space"></span><span id="process_privileged_virtual_address_space"></span><span id="PROCESS_PRIVILEGED_VIRTUAL_ADDRESS_SPACE"></span>处理特权虚拟地址空间


使用磁贴资源的进程会在首次调用 [*ReserveGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb)时获取与它们关联的另一个虚拟地址空间。 此地址空间用于通过呈现以同步方式更新进程的页表。 我们在 [磁贴资源](tile-resources.md) 主题中介绍了这一地址空间。

## <a name="span-idvirtual_address_space_on_linked_display_adaptersspanspan-idvirtual_address_space_on_linked_display_adaptersspanspan-idvirtual_address_space_on_linked_display_adaptersspanvirtual-address-space-on-linked-display-adapters"></a><span id="Virtual_address_space_on_linked_display_adapters"></span><span id="virtual_address_space_on_linked_display_adapters"></span><span id="VIRTUAL_ADDRESS_SPACE_ON_LINKED_DISPLAY_ADAPTERS"></span>链接的显示适配器上的虚拟地址空间


如果物理图形适配器链接到链接的显示适配器链，则每个进程仍有一个 GPU 虚拟地址空间 (除了页面进程) 。 但每个物理适配器上的虚拟地址空间是由其自己的一组页表映射的。

 

