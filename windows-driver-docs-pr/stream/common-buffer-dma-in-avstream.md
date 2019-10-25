---
title: AVStream 中的常见缓冲区 DMA
description: AVStream 中的常见缓冲区 DMA
ms.assetid: 8cbadb5a-f879-4fe0-a698-cde3b9f6df83
keywords:
- 常见缓冲区 DMA WDK AVStream
- 缓冲区 WDK AVStream
- AVStream WDK，硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6dbb52d010b13e74c4312c496dfb5f36ec90e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844715"
---
# <a name="common-buffer-dma-in-avstream"></a>AVStream 中的常见缓冲区 DMA





当设备不直接写入捕获缓冲区时，会发生公用缓冲区直接内存访问（DMA）;相反，它会将数据复制到公共缓冲区和从中复制数据。

在 AVStream 微型驱动程序中使用通用缓冲区 DMA：

1.  调用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来获取 DMA 适配器，就像在基于数据包的 DMA 中一样。 不要指定 KSPIN\_标记\_在[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)的**FLAGS**成员\_EX 结构中生成\_映射，并且不要将 DMA 适配器注册到 AVStream。 可能需要实现自己的专用缓冲区/复制方案。

2.  如[编写硬件的 AVStream 微型驱动程序](writing-avstream-minidrivers-for-hardware.md)中所述，注册中断服务例程（ISR）

如果 KSPIN 的**Flags**成员\_描述符\_EX 集 KSPIN\_标志\_\_\_\_进行处理，则在 AVStream 调用[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)之前执行以下步骤：

1.  微型驱动程序设置其常见的缓冲区传输。

2.  内核将调用供应商以前注册的 ISR。 在 ISR 中，微型驱动程序对延迟的过程调用（DPC）进行排队。

3.  当公用缓冲区已满时，微型驱动程序从 DPC 调用[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing) 。

4.  如果满足[**KSPIN\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)的**Flags**成员指定的条件，AVStream 将调用进程调度\_EX。

在供应商提供的[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)回调例程中，一种可能的操作过程如下所示：

1.  调用[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)：

    ```cpp
    KSSTREAM_POINTER *Leading = KsPinGetLeadingEdgeStreamPointer (
                    Pin,
                    State
                   );
    ```

2.  将帧数据复制到&gt;StreamHeader 的&gt;数据，并在相应的[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)中设置必要的标志和时间戳信息。

3.  调用[**KsStreamPointerUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)并将*Eject*设置为**TRUE**。 （此*弹出*的值会导致流指针前进。）

4.  返回状态\_挂起。

然后，AVStream 根据[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构中的微型驱动程序设置的标志来管理队列。

 

 




