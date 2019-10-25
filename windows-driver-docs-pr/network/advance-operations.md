---
title: 前进操作
description: 前进操作
ms.assetid: 42554221-201d-4014-900d-435a47b3afa1
keywords:
- 网络数据 WDK，高级操作
- 数据 WDK 网络，高级操作
- 包 WDK 网络，高级操作
- 高级操作 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- 释放 MDLs
- 减少使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3dd93025b08dae8f6e8fd7a01431e7a8699c87b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838236"
---
# <a name="advance-operations"></a>前进操作





高级操作将[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构或 NET [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中所有 net\_缓冲区结构中的已用数据空间减小。

驱动程序使用以下高级功能：

[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)

[**NdisAdvanceNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferlistdatastart)

高级操作有时可以释放与 NET\_BUFFER 结构关联的 MDLs。 为提供释放 MDLs 的机制，驱动程序可以为[**NetFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_free_mdl_handler)函数提供可选的入口点。 如果入口点为**NULL**，NDIS 将使用默认方法来分配 MDLs。 MDLs 只能在*NetFreeMdl*中使用与用于在[**NetAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_allocate_mdl_handler)函数中分配 MDL 的机制互惠相同的机制来释放。

为了获取新的**DataLength**，NDIS 从当前**DataLength**中减去驱动程序指定的*DataOffsetDelta* 。 如果上一个撤回操作分配了新的数据空间，则提前操作可释放此类之前分配的内存。 如果高级操作不能释放内存，NDIS 只需将*DataOffsetDelta*添加到当前**数据偏移量**即可获得新的**数据偏移量**。 如果高级操作释放了内存，NDIS 会相应地调整**数据偏移量**。

对于 send complete 事例，高级操作可释放以前的撤回操作中分配的内存。 为了获得更好的性能，驱动程序应在发送之前分配足够的总数据大小，以容纳所有底层驱动程序的撤回操作。

对于接收指示事例，高级操作只需相应地调整**数据偏移量**和**DataLength** 。 前进操作完成后，较低层的标头将保留在*未使用的数据空间*中。

 

 





