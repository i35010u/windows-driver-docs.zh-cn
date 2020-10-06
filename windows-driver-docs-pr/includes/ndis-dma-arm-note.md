---
description: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
title: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.topic: include
ms.openlocfilehash: bbefcca96af58fadedad695f7bf1222c94d753b8
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91745506"
---
> [!CAUTION]
> 对于 ARM 和 ARM64 处理器，强烈建议 NDIS 驱动程序编写器使用 WDF DMA 或 WDM DMA，而不是使用 NDIS 散播/聚集 DMA。
>
> 有关 WDF DMA 的详细信息，请参阅 [在 KMDF 驱动程序中处理 DMA 操作](../wdf/introduction-to-dma-in-windows-driver-framework.md)。
>
> 有关 WDM DMA 的详细信息，请参阅 [管理驱动程序的输入/输出](../kernel/handling-irps.md)的与 DMA 相关的子主题。