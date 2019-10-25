---
title: 供应和回收更改
description: 对于 Windows 显示驱动程序模型（WDDM） v2，有关产品/服务和回收的要求将被放松。
ms.assetid: 1A987708-DE73-4998-B5F9-03A9D502205A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce81472b86ae091ee7cd5e1e7450035c92e54427
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840502"
---
# <a name="offer-and-reclaim-changes"></a>供应和回收更改


对于 Windows 显示驱动程序模型（WDDM） v2，有关*产品/服务*和*回收*的要求将被放松。 用户模式驱动程序不再需要在内部分配中使用产品/服务和回收。 空闲/挂起的应用程序将使用 Microsoft DirectX 11.1 中引入的**剪裁**API 来消除驱动程序内部资源。

在 API 级别继续支持产品/服务和回收，需要用户模式驱动程序来转发应用程序请求，以便向内核提供或回收资源。 在 WDDM v2 下，将不再支持通过分配列表提供的服务分配，因此，用户模式驱动程序需要更改其实现产品/服务的方式。

如果资源在当前在所有上下文中生成的直接内存访问（DMA）缓冲区中没有**引用，则**由用户模式驱动程序立即提供应用程序提供的资源。 如果资源在正在生成的 DMA 缓冲区中有挂起的引用，则用户模式驱动程序应将对**OfferCb**的调用推迟到通过[*RENDERCB*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)提交依赖 DMA 缓冲区之后。 图形内核将负责以非阻止方式延迟操作，直到能够安全地提供资源，这样，用户模式驱动程序无需担心必须推迟对**OfferCb**的调用，直到依赖操作完成在图形处理单元（GPU）上。

如果调用了驻留要求列表（即，用户或驱动程序已请求通过[*MakeResidentCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)调用进行分配），则调用回收会自动在分配中分页。 对于[**ReclaimAllocations2Cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)，此操作是异步的，并且会返回分页防护，其处理方式与从*MakeResidentCb*返回的隔离方式相同。 此分配可保证为常驻，并在向其发出防护时在 GPU 上可用。

从[**ReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)/[**ReclaimAllocations2Cb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations2cb)返回后，将保证分配的后备存储有效，并可通过[*Lock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)将分配置于 CPU 访问下。 驱动程序无需等待分页防护。

 

 





