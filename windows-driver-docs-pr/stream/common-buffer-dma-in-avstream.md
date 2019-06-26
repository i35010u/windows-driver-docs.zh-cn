---
title: AVStream 中的常见缓冲区 DMA
description: AVStream 中的常见缓冲区 DMA
ms.assetid: 8cbadb5a-f879-4fe0-a698-cde3b9f6df83
keywords:
- 常见缓冲区 DMA WDK AVStream
- 缓冲区 WDK AVStream
- AVStream WDK 硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92534fc14617978eb76b8ad5f6350724ecfee4a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386652"
---
# <a name="common-buffer-dma-in-avstream"></a>AVStream 中的常见缓冲区 DMA





设备不会直接写入捕获缓冲区中; 时发生常见缓冲区直接内存访问 (DMA)而是它将数据复制到和从常见的缓冲区。

若要使用你 AVStream 微型驱动程序中的常见缓冲区 DMA:

1.  通过调用获取 DMA 适配器[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)，如下所示基于数据包的 DMA。 未指定 KSPIN\_标志\_生成\_中的映射**标志**隶属[ **KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构，并且不向 AVStream 注册 DMA 适配器。 您可能需要实施自己的专用缓冲区/复制方案。

2.  注册中断服务例程 (ISR) 中所述[编写 AVStream 微型驱动程序硬件](writing-avstream-minidrivers-for-hardware.md)

如果**标志**KSPIN 成员\_描述符\_EX 设置 KSPIN\_标志\_执行\_不\_启动\_处理以下AVStream 调用之前发生的步骤[ *AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin):

1.  微型驱动程序设置了其常见的缓冲区传输。

2.  内核调用供应商以前已注册 ISR。 在 ISR，微型驱动程序队列的延迟的过程调用 (DPC)。

3.  微型驱动程序时常见的缓冲区已满时，调用[ **KsPinAttemptProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattemptprocessing)从 DPC。

4.  如果通过指定条件，AVStream 调用进程调度**标志**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)满足。

中的供应商提供[ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)回调例程，一个可能的操作过程，如下所示：

1.  调用[ **KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer):

    ```cpp
    KSSTREAM_POINTER *Leading = KsPinGetLeadingEdgeStreamPointer (
                    Pin,
                    State
                   );
    ```

2.  将帧数据复制到前导-&gt;StreamHeader-&gt;数据和设置所需的标志和时间戳信息在相应[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)。

3.  调用[ **KsStreamPointerUnlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)与*弹出*设置为**TRUE**。 (此值的*弹出*会导致流指针前进。)

4.  返回状态\_PENDING。

然后，AVStream 管理基于由微型驱动程序中设置的标志的队列[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。

 

 




