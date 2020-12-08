---
title: 供应和回收更改
description: 对于 Windows 显示器驱动程序模型 (WDDM) v2，有关产品/服务和回收的要求将被放松。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64d2bfcb0d3dcfb02b70e8e141233ea8715b9bac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841271"
---
# <a name="offer-and-reclaim-changes"></a>供应和回收更改


对于 Windows 显示器驱动程序模型 (WDDM) v2，有关 *产品/服务* 和 *回收* 的要求将被放松。 用户模式驱动程序不再需要在内部分配中使用产品/服务和回收。 空闲/挂起的应用程序将使用 Microsoft DirectX 11.1 中引入的 **剪裁** API 来消除驱动程序内部资源。

在 API 级别继续支持产品/服务和回收，需要用户模式驱动程序来转发应用程序请求，以便向内核提供或回收资源。 在 WDDM v2 下，将不再支持通过分配列表提供的服务分配，因此，用户模式驱动程序需要更改其实现产品/服务的方式。

应用程序提供的资源应该由用户模式驱动程序立即提供，方法是调用 **OfferCb**，前提是资源在直接内存访问中没有引用 (DMA) 当前在所有上下文中生成的缓冲区。 如果资源在正在生成的 DMA 缓冲区中有挂起的引用，则用户模式驱动程序应将对 **OfferCb** 的调用推迟到通过 [*RENDERCB*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)提交依赖 DMA 缓冲区之后。 图形内核将以非阻止方式处理延迟操作，直到能够安全地提供资源，这样，用户模式驱动程序无需担心在 (GPU) 的图形处理单元上完成相关操作之前必须将对 **OfferCb** 的调用推迟。

如果调用回收在驻留要求列表中，则调用 "回收" 将自动在分配中分页 (即，用户或驱动程序已请求通过 [*MakeResidentCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) 调用) 进行分配。 对于 [**ReclaimAllocations2Cb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)，此操作是异步的，并且会返回分页防护，其处理方式与从 *MakeResidentCb* 返回的隔离方式相同。 此分配可保证为常驻，并在向其发出防护时在 GPU 上可用。

从 [**ReclaimAllocationsCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb) / [**ReclaimAllocations2Cb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)返回后，可以立即确保分配的后备存储有效，并可通过 [*Lock2Cb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)将分配置于 CPU 访问下。 驱动程序无需等待分页防护。

 

