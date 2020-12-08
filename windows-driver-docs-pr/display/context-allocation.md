---
title: 上下文分配
description: 若要为上下文的上下文保存区分配内存，内核模式驱动程序可以通过 DxgkCbCreateContextAllocation 使用上下文分配。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9306c26e90f651b6df37a0426ba9c5c7135dfad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810149"
---
# <a name="context-allocation"></a>上下文分配


若要为上下文的上下文保存区分配内存，内核模式驱动程序可以通过 [*DxgkCbCreateContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)使用上下文分配。 在上下文分配中添加了一些新功能，以使它们适合新的图形处理单元 (GPU) 虚拟地址模型。

## <a name="span-idaccessedphysicallyspanspan-idaccessedphysicallyspanspan-idaccessedphysicallyspanaccessedphysically"></a><span id="AccessedPhysically"></span><span id="accessedphysically"></span><span id="ACCESSEDPHYSICALLY"></span>AccessedPhysically


上下文分配可以指定 **AccessedPhysically** 标志，以指示应在内存段中连续分配分配，或在从系统内存访问时将分配映射到口径。

## <a name="span-idassigning_a_gpu_virtual_address_to_a_context_allocationspanspan-idassigning_a_gpu_virtual_address_to_a_context_allocationspanspan-idassigning_a_gpu_virtual_address_to_a_context_allocationspanassigning-a-gpu-virtual-address-to-a-context-allocation"></a><span id="Assigning_a_GPU_virtual_address_to_a_context_allocation"></span><span id="assigning_a_gpu_virtual_address_to_a_context_allocation"></span><span id="ASSIGNING_A_GPU_VIRTUAL_ADDRESS_TO_A_CONTEXT_ALLOCATION"></span>将 GPU 虚拟地址分配给上下文分配


视频内存管理器向内核模式驱动程序公开新的 [*DxgkCbMapContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_mapcontextallocation) 服务，以便将 GPU 虚拟地址分配给上下文分配。

上下文分配将映射到与指定上下文关联的应用程序 GPU 虚拟地址空间。

**注意**  当上下文分配直接映射到应用程序 GPU 虚拟地址空间时，驱动程序应注意不要公开特权信息。

 

这些服务的行为类似于其用户模式对应项。

## <a name="span-idupdating_the_content_of_a_context_allocationspanspan-idupdating_the_content_of_a_context_allocationspanspan-idupdating_the_content_of_a_context_allocationspanupdating-the-content-of-a-context-allocation"></a><span id="Updating_the_content_of_a_context_allocation"></span><span id="updating_the_content_of_a_context_allocation"></span><span id="UPDATING_THE_CONTENT_OF_A_CONTEXT_ALLOCATION"></span>更新上下文分配的内容


内核模式驱动程序在某些时候可能需要更新上下文分配的内容。 例如，特权 (**AccessedPhysically**，任何 GPU 虚拟映射) 上下文分配可能包含对与特定上下文相关联的页面目录的引用。 当 [*DxgkDdiSetRootPageTable*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)内核模式驱动程序收到页面目录重定位的通知时，内核模式驱动程序可能需要更新该上下文分配的内容。

出于此目的，添加了一个新的 [*DxgkCbUpdateContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_updatecontextallocation)设备驱动程序接口 (DDI) 。 此 DDI 将对视频内存管理器的请求排队，以启动上下文分配的更新。 要更新的上下文分配将映射到视频内存管理器分页过程的空闲区，然后使用新的 *UpdateContextAllocation* 分页操作调用该驱动程序，以执行上下文分配的实际更新。 更新完成后，视频内存管理器从 *DxgkCbUpdateContextAllocation* 返回。

内核模式驱动程序可在其对 [*DxgkCbUpdateContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_updatecontextallocation) 的调用和生成的 *UpdateContextAllocation* 分页操作之间传递某些专用驱动程序数据。

 

