---
title: 新的分散/聚合 DMA 支持
description: 新的分散/聚合 DMA 支持
keywords:
- 散播/聚集 DMA WDK 网络
- 微型端口驱动程序 WDK 网络，散点/集合 DMA
- NDIS 微型端口驱动程序 WDK、散播/聚集 DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9705bf1db446cd3a8a01018e1b23b9a60b878daa
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247938"
---
# <a name="new-scattergather-dma-support"></a>新的分散/聚合 DMA 支持





与以前版本的 NDIS 不同，NDIS 6.0 在为 DMA 传输映射数据包之前，会将发送数据包传递到微型端口驱动程序。 获取数据包后，微型端口驱动程序可以请求 NDIS 为数据包提供散播/聚集列表。

这提供了以下好处：

-   由于微型端口驱动程序在映射之前有权访问数据包，因此，微型端口驱动程序对数据包所做的任何更改都会反映在关联的分散/收集列表数据中。

-   微型端口驱动程序可以通过将小型数据包或非常零碎的数据包复制到预分配的缓冲区来优化传输，从而无需进行映射。 这消除了不必要的处理。

-   NDIS 可以在一个函数调用中将多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构安全地传递给微型端口驱动程序。 这会减少对微型端口驱动程序的调用，从而提高系统性能。

-   由于微型端口驱动程序可以为散点/集合列表预分配内存，因此在运行时，NDIS 不必为散点/集合列表分配内存。

有关 NDIS 6.0 散播/聚集 DMA 的详细信息，请参阅 [ndis 6.0 散播/聚集 dma](ndis-scatter-gather-dma.md)。

 

