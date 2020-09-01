---
title: AVStream 中基于数据包的 DMA
description: AVStream 中基于数据包的 DMA
ms.assetid: 4246819e-d8d6-4302-9477-675ca181b1e3
keywords:
- AVStream WDK，硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 基于数据包的 DMA WDK AVStream
- 散播/聚集 DMA WDK AVStream
- 捕获缓冲区 WDK AVStream
- 缓冲区 WDK AVStream
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: a5106f01bf233ae4c4e1f255b16b9d31e6f2eabb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183945"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream 中基于数据包的 DMA

当微型驱动程序直接从中读取数据并直接写入数据以捕获从用户模式接收的缓冲区时，将会进行基于数据包的直接内存访问 (DMA) 。 Windows 驱动程序工具包中的 [AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/) (WDK) 示例演示如何生成执行此类 DMA 的 AVStream 微型驱动程序。

实现基于数据包的 DMA 方案：

1. 指定 KSPIN \_ 标志 \_ 会 \_ 在相关[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的**Flags**成员中生成映射。 请注意，此标志仅应由具有散点/集合支持的总线主机使用。

1.  (ISR 注册中断服务例程) 如 [编写硬件的 AVStream 微型驱动程序](writing-avstream-minidrivers-for-hardware.md)中所述。

然后，在 [*AVStrMiniDeviceStart*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicepnpstart) 启动调度：

1. 使用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)设置 DMA 适配器对象。

1. 通过调用 [**KsDeviceRegisterAdapterObject**](/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)，将 DMA 适配器对象注册到 AVStream。

微型驱动程序通过在对[**KsDeviceRegisterAdapterObject**](/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)的调用中提供*MaxMappingByteCount*参数来指定单个散点/集合映射的最大大小。

如果任何散点/集合映射超出了此最大大小，则 AVStream 会自动将映射拆分为多个散点/集合映射，每个映射的大小不能大于在 *MaxMappingByteCount*中指定的大小。

还必须提供 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin) 回调例程。 驱动程序编写器应为此回调选择合适的功能。 例如，你可以执行以下操作：

1. 调用 [**KsPinGetLeadingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)。

1. 通过调用 [**KsStreamPointerClone**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)克隆前导边缘。

1. 基于克隆的计划 DMA 硬件。

1. 调用 [**KsStreamPointerAdvanceOffsets**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets) 或 [**KsStreamPointerAdvance**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvance) 来前进领先的边缘。

1. 根据需要对其他帧重复步骤2。

当硬件中断用于 DMA 完成时，内核将调用供应商以前注册的 ISR。 在 ISR 中，微型驱动程序将延迟的过程调用排队 (DPC) 。

DPC 应更新 **DataUsed** ，并且可能更新 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header) 结构的其他成员。 然后，DPC 可以调用 [**KsStreamPointerDelete**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete) 来删除克隆并释放关联的帧。

或者，如果只是部分帧完成，则 DPC 可能会前进克隆指针。 为此，请调用 [**KsStreamPointerAdvanceOffsets**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)。

如果需要恢复处理，请调用 [**KsPinAttemptProcessing**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)。

> [!NOTE]
> 如果映射的长度小于一个物理页，则不能保证它驻留在单个物理页上。