---
title: 请注意，若要不鼓励使用 ARM/ARM64 的处理器上的 NDIS DMA 使用
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bacadff06277b9cfb4816cdde57c0653775ea863
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535013"
---
> [!CAUTION]
> 对于 ARM 和 ARM64 处理器，我们强烈建议 NDIS 驱动程序编写人员而不是 NDIS 散播-聚集 DMA 使用 WDF DMA 或 WDM DMA。 
>
> WDF DMA 的详细信息，请参阅[KMDF 驱动程序中处理 DMA 操作](../wdf/handling-dma-operations-in-kmdf-drivers.md)。
>
> 有关 WDM DMA 的详细信息，请参阅 DMA 相关子主题的[驱动程序管理输入/输出](../kernel/managing-input-output-for-drivers.md)。
