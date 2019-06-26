---
title: 前进操作
description: 前进操作
ms.assetid: 42554221-201d-4014-900d-435a47b3afa1
keywords:
- 网络数据 WDK，提前操作
- 数据 WDK 网络，提前操作
- 数据包 WDK 网络，提前操作
- 高级操作 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- 释放 MDLs
- 减少使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 188bc3d019608b365cdd84391df91347c3021910
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382924"
---
# <a name="advance-operations"></a>前进操作





高级操作减少中使用的数据空间的大小[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构或在所有 NET\_缓冲区中结构[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

驱动程序使用以下高级功能：

[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisadvancenetbufferdatastart)

[**NdisAdvanceNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisadvancenetbufferlistdatastart)

高级操作有时可以释放与网络相关联的 MDLs\_缓冲区结构。 若要提供用于释放 MDLs 的机制，驱动程序可以提供的可选入口点[ **NetFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-net_buffer_free_mdl_handler)函数。 如果入口点是**NULL**，NDIS 使用默认方法来分配 MDLs。 必须仅在释放 MDLs *NetFreeMdl*使用的机制，用于分配在 MDL 该倒数[ **NetAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-net_buffer_allocate_mdl_handler)函数。

若要获取的新**DataLength**，NDIS 中减去的驱动程序指定*DataOffsetDelta*从当前**DataLength** 。 如果以前的参加操作分配新的数据空间，则高级操作可以释放此类之前分配的内存。 如果提前操作不会释放内存，只需添加 NDIS *DataOffsetDelta*与当前**DataOffset**以获取新**DataOffset** 。 如果提前操作已释放的内存，调整 NDIS **DataOffset**相应地。

对于发送的完成情况，提前操作可以释放以前撤回操作中所分配的内存。 为了提高性能，驱动程序应以容纳所有基础驱动程序的参加操作在发送之前分配足够的总数据大小。

接收指示的情况下，高级操作只需调整**DataOffset**并**DataLength**相应地。 提前完成操作后，较低层的标头将保留在*未使用的数据空间*。

 

 





