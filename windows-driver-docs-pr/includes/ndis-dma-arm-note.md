---
description: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
title: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.topic: include
ms.openlocfilehash: eb0e1fa3152435ab7d8b97f00e580091ef626e12
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811995"
---
# <a name="note-to-discourage-ndis-dma-use-on-armarm64-processors"></a>阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项

> [!CAUTION]
> 对于 ARM 和 ARM64 处理器，强烈建议 NDIS 驱动程序编写器使用 WDF DMA 或 WDM DMA，而不是使用 NDIS 散播/聚集 DMA。
>
> 有关 WDF DMA 的详细信息，请参阅 [在 KMDF 驱动程序中处理 DMA 操作](../wdf/handling-dma-operations-in-kmdf-drivers.md)。
>
> 有关 WDM DMA 的详细信息，请参阅 [管理驱动程序的输入/输出](../kernel/managing-input-output-for-drivers.md)的与 DMA 相关的子主题。
