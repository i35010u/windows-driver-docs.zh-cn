---
description: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
title: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c8c8abf11042b302c72e1d51e1dcef674d0cb141
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042816"
---
# <a name="note-to-discourage-ndis-dma-use-on-armarm64-processors"></a>阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项

> [!CAUTION]
> 对于 ARM 和 ARM64 处理器，强烈建议 NDIS 驱动程序编写器使用 WDF DMA 或 WDM DMA，而不是使用 NDIS 散播/聚集 DMA。
>
> 有关 WDF DMA 的详细信息，请参阅 [在 KMDF 驱动程序中处理 DMA 操作](../wdf/handling-dma-operations-in-kmdf-drivers.md)。
>
> 有关 WDM DMA 的详细信息，请参阅 [管理驱动程序的输入/输出](../kernel/managing-input-output-for-drivers.md)的与 DMA 相关的子主题。
