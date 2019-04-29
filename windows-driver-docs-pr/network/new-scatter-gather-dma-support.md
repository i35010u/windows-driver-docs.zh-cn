---
title: 新的分散/聚合 DMA 支持
description: 新的分散/聚合 DMA 支持
ms.assetid: ac7cd98b-1211-4538-a54b-7362fa1d81b0
keywords:
- 散播-聚集 DMA WDK 网络
- 微型端口驱动程序 WDK 网络、 散播-聚集 DMA
- NDIS 微型端口驱动程序 WDK，散播-聚集 DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a64a234cf49067a47d0bbc224329c29448c616cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380591"
---
# <a name="new-scattergather-dma-support"></a>新的分散/聚合 DMA 支持





与以前版本的 NDIS，不同 NDIS 6.0 之前将传递发送数据包给微型端口驱动程序为 DMA 传输映射该数据包。 获取数据包后，微型端口驱动程序可以请求 NDIS 提供数据包的分散/集中列表。

这提供了以下好处：

-   微型端口驱动程序有权访问该数据包之前对其进行映射,，因为微型端口驱动程序对数据包进行任何更改都反映在关联的散播-聚集列表数据。

-   微型端口驱动程序可以通过将其复制到的预先分配的缓冲区，从而不必映射进行优化的小型或高分段的数据包的传输。 这消除了不必要的处理。

-   NDIS 安全地传递多个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)到一个函数调用中的微型端口驱动程序的结构。 这会导致较少调用微型端口驱动程序，因而提高系统性能。

-   由于微型端口驱动程序可以预分配散播-聚集列表的内存，则不需要在运行时为散播-聚集列表分配内存 NDIS。

NDIS 6.0 散播-聚集 DMA 的详细信息，请参阅[NDIS 6.0 散播-聚集 DMA](ndis-scatter-gather-dma.md)。

 

 





