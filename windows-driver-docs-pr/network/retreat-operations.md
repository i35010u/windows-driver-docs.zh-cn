---
title: 重新处理操作
description: 重新处理操作
keywords:
- 网络数据 WDK，撤回操作
- 数据 WDK 网络，撤回操作
- 包 WDK 网络，撤回操作
- 撤回操作 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- 分配 MDLs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b94748530dfd378fa75300b4fa33a033b2cb1e1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838553"
---
# <a name="retreat-operations"></a>重新处理操作





撤回操作可以增加 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构中的已用数据空间的大小，也可以增加 \_ [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中所有网络缓冲区结构的大小。

NDIS 提供以下撤回函数：

[**NdisRetreatNetBufferDataStart**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)

[**NdisRetreatNetBufferListDataStart**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferlistdatastart)

撤回操作有时可以分配与网络缓冲区结构关联的 MDLs \_ 。 为提供分配 MDLs 的机制，驱动程序可以为 [**NetAllocateMdl**](/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_allocate_mdl_handler) 函数提供可选的入口点。 如果入口点为 **NULL**，NDIS 将使用默认方法来分配 MDLs。 MDLs 必须在提供用于分配 MDL 的机制的倒数的 [**NetFreeMdl**](/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_free_mdl_handler) 函数内释放。

为获取新的 **DataLength**，NDIS 会将驱动程序指定的 *DataOffsetDelta* 添加到当前 **DataLength** 。 如果 *未使用的数据空间* 的大小大于 *DataOffsetDelta*，则撤回操作将减少 **数据偏移量** 。 在这种情况下，新的 **数据偏移量** 为当前 **数据偏移量** 减 *DataOffsetDelta* 。

如果 *DataOffsetDelta* 大于 **数据偏移量**，则撤回操作会分配新数据空间。 在这种情况下，NDIS 会相应地调整 **数据偏移量** 。

对于发送操作，如果没有足够的 *未使用数据空间* 来满足撤回请求，NDIS 会分配内存。 如果不需要内存分配，NDIS 只需调整 **数据偏移量** 和 **DataLength** 。 为了获得更好的性能，驱动程序应在发送之前分配足够的总数据大小，以容纳所有底层驱动程序的撤回操作。

对于接收返回事例，NDIS 只需相应地调整 **数据偏移量** 和 **DataLength** 。 撤回操作会反转接收处理期间发生的高级操作。 撤回操作完成后，所 *用的数据空间* 包含基础驱动程序在接收处理期间使用的标头数据。

 

