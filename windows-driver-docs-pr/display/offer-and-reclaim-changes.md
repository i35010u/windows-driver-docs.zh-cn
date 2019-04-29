---
title: 供应和回收更改
description: Windows 显示器驱动程序模型 (WDDM) v2 是正在放宽要求产品/服务和回收。
ms.assetid: 1A987708-DE73-4998-B5F9-03A9D502205A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12a3a0e7f72c6fec26bc232e13ca9803df7c48ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383995"
---
# <a name="offer-and-reclaim-changes"></a>供应和回收更改


对于 Windows 显示器驱动程序模型 (WDDM) v2，规定*产品/服务*和*回收*正在放宽了。 用户模式驱动程序不再需要使用产品/服务，并在内部分配上回收。 空闲/已挂起应用程序将使用的驱动程序内部资源消除**剪裁**Microsoft DirectX 11.1 中引入的 API。

产品/服务和回收将继续支持在 API 级别和用户模式驱动程序所需转发产品/服务或回收对内核的资源的应用程序请求。 WDDM v2，通过分配列表不再支持产品/服务分配，因此用户模式驱动程序所需更改的方式，它将实现产品/服务并回收。

资源提供的应用程序应提供立即由用户模式驱动程序通过调用**OfferCb**，如果资源在所有当前正在生成的直接内存访问 (DMA) 缓冲区中有没有引用上下文。 如果资源具有挂起的所生成的 DMA 缓冲区中的引用，用户模式驱动程序应延迟到调用**OfferCb**直到通过提交依赖 DMA 缓冲区后[ *RenderCb*](https://msdn.microsoft.com/library/windows/hardware/ff568923). 将推迟到该操作，以非阻止方式，则可以安全地提供资源，这种情况下用户模式驱动程序无需担心是否有将延迟到调用处理图形内核**OfferCb**之前图形处理单元 (GPU) 上完成相关操作。

它是驻留要求列表中，调用回收将自动分页在分配中 (即用户或驱动程序已请求分配通过驻留[ *MakeResidentCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906357)调用)。 有关[ **ReclaimAllocations2Cb**](https://msdn.microsoft.com/library/windows/hardware/dn903528)，此操作是异步的以及分页 fence 返回，并且其处理方式与从返回的界定相同*MakeResidentCb*. 分配被保证时发出信号 fence 可以驻留和 GPU 上可用。

从返回后立即[ **ReclaimAllocationsCb**](https://msdn.microsoft.com/library/windows/hardware/hh451695)/[**ReclaimAllocations2Cb**](https://msdn.microsoft.com/library/windows/hardware/dn903528)，后备存储保证是有效分配和分配可能会放置在通过 CPU 访问下[ *Lock2Cb*](https://msdn.microsoft.com/library/windows/hardware/dn914483)。 该驱动程序不需要等待分页 fence，若要执行此操作。

 

 





