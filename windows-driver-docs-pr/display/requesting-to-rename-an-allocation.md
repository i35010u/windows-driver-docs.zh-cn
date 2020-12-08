---
title: 请求重命名分配
description: 请求重命名分配
keywords:
- 命令缓冲区 WDK 显示，分配重命名
- DMA 缓冲区 WDK 显示，分配重命名
- 分配重命名 WDK 显示
- 重命名分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f037b96246297a726964f72834c38fc1824171c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808881"
---
# <a name="requesting-to-rename-an-allocation"></a>请求重命名分配


用户模式显示驱动程序应该请求当应用程序指示在锁定图面的请求过程中丢弃图面内容时，视频内存管理器会重命名与图面关联的分配 (例如，顶点缓冲区) 。 Microsoft Direct3D 运行时传递 **放弃** 位字段标志，以指示该标志不再需要当前的图面内容。 如果当前分配的包含图面内容的当前分配处于繁忙状态，而不是停止应用程序线程，则该驱动程序可以请求在当前分配空闲之前，视频内存管理器分配一个新分配来处理锁请求。

用户模式显示驱动程序请求当驱动程序在对 [**pfnLockCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数的调用中设置 [**D3DDDICB \_ LOCKFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)结构的 **丢弃** 成员时，视频内存管理器会重命名分配。 视频内存管理器会确定它是否应该重命名分配，或是否应该导致应用程序停止，直到分配处于空闲状态（根据分配当前是否繁忙）以及当前内存情况。 对于正在重命名的每个分配，视频内存管理器会维护一组连续用于锁定分配的分配。 每次应用程序放弃分配内容时，视频内存管理器都会循环遍历列表。 列表的长度由应用程序要求和内存压力决定。 视频内存管理器尝试使列表足够长，以避免在锁定请求上停止应用程序线程。 但是，在内存压力下，视频内存管理器可以剪裁列表，以免导致额外的内存压力。

若要对分配的重命名列表的长度施加限制，驱动程序会在创建分配时设置 [**DXGK \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的 **MaximumRenamingListLength** 成员。 如果驱动程序将 **MaximumRenamingListLength** 设置为非零值，则视频内存管理器将确定重命名列表的适当长度，而不会超过驱动程序施加的限制。 如果驱动程序将 **MaximumRenamingListLength** 设置为0，则内存管理器可以将重命名列表的大小增加到需要的任何大小以提高性能。

请注意，当用户模式显示驱动程序设置 [**D3DDDICB \_ LOCKFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)的 **丢弃** 成员时，视频内存管理器不会调用显示微型端口驱动程序为原始分配分配额外分配。 视频内存管理器使用原始分配的创建参数来创建所有额外分配。 从显示微型端口驱动程序的角度来看，相同的分配在可能多个同时分段位置上分页。

 

