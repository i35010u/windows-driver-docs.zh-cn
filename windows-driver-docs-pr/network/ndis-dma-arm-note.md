---
title: 阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 32310496340d59aa8696625e9535743de516a24e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75297308"
---
# <a name="note-to-discourage-ndis-dma-use-on-armarm64-processors"></a>阻止在 ARM/ARM64 处理器上使用 NDIS DMA 的注意事项

> [!CAUTION]
> 对于 ARM 和 ARM64 处理器，强烈建议 NDIS 驱动程序编写器使用 WDF DMA 或 WDM DMA，而不是使用 NDIS 散播/聚集 DMA。
>
> 有关 WDF DMA 的详细信息，请参阅[在 KMDF 驱动程序中处理 DMA 操作](../wdf/handling-dma-operations-in-kmdf-drivers.md)。
>
> 有关 WDM DMA 的详细信息，请参阅[管理驱动程序的输入/输出](../kernel/managing-input-output-for-drivers.md)的与 DMA 相关的子主题。
