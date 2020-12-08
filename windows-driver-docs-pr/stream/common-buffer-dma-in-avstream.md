---
title: AVStream 中的常见缓冲区 DMA
description: AVStream 中的常见缓冲区 DMA
keywords:
- 常见缓冲区 DMA WDK AVStream
- 缓冲区 WDK AVStream
- AVStream WDK，硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e5ccc481869012d71fd82048ea357b093a17907
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813455"
---
# <a name="common-buffer-dma-in-avstream"></a>AVStream 中的常见缓冲区 DMA





当设备不直接写入捕获缓冲区时， (DMA) 的常见缓冲区直接内存访问;相反，它会将数据复制到公共缓冲区和从中复制数据。

在 AVStream 微型驱动程序中使用通用缓冲区 DMA：

1.  调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来获取 DMA 适配器，就像在基于数据包的 DMA 中一样。 不要指定 KSPIN \_ 标志 \_ \_ 在 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **Flags** 成员中生成映射，并且不要将 DMA 适配器注册到 AVStream。 可能需要实现自己的专用缓冲区/复制方案。

2.   (ISR 注册中断服务例程) 如[编写硬件的 AVStream 微型驱动程序](writing-avstream-minidrivers-for-hardware.md)中所述

如果 KSPIN **Flags** \_ 说明符 \_ EX Sets KSPIN 标志的 Flags 成员 \_ \_ \_ 未 \_ 启动 \_ 处理，则在 AVStream 调用 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)之前执行以下步骤：

1.  微型驱动程序设置其常见的缓冲区传输。

2.  内核将调用供应商以前注册的 ISR。 在 ISR 中，微型驱动程序将延迟的过程调用排队 (DPC) 。

3.  当公用缓冲区已满时，微型驱动程序从 DPC 调用 [**KsPinAttemptProcessing**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing) 。

4.  如果满足 [**KSPIN \_ 描述符的 \_**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) **Flags** 成员指定的条件，AVStream 将调用进程调度。

在供应商提供的 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin) 回调例程中，一种可能的操作过程如下所示：

1.  调用 [**KsPinGetLeadingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)：

    ```cpp
    KSSTREAM_POINTER *Leading = KsPinGetLeadingEdgeStreamPointer (
                    Pin,
                    State
                   );
    ```

2.  将帧数据复制到 &gt; StreamHeader &gt; 数据，并在相应的 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)中设置所需的标志和时间戳信息。

3.  调用 [**KsStreamPointerUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock) 并将 *Eject* 设置为 **TRUE**。  (此 *弹出* 的值会导致流指针前进。 ) 

4.  返回状态为 " \_ 挂起"。

然后，AVStream 根据微型驱动程序在 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 结构中设置的标志来管理队列。

 

