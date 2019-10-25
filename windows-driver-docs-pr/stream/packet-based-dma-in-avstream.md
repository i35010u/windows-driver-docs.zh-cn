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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eb62c7d719d14655f6f20f8a06e5da9f674d7af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823511"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream 中基于数据包的 DMA





当你的微型驱动程序直接从读取数据并直接写入数据以捕获从用户模式接收的缓冲区时，将发生基于数据包的直接内存访问（DMA）。 Windows 驱动程序工具包示例中的[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)演示了如何生成执行此类 DMA 的 AVStream 微型驱动程序。

实现基于数据包的 DMA 方案：

1.  指定 KSPIN\_标记\_在相关的[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)的**FLAGS**成员中生成\_映射\_EX 结构。 请注意，此标志仅应由具有散点/集合支持的总线主机使用。

2.  如[编写硬件的 AVStream 微型驱动程序](writing-avstream-minidrivers-for-hardware.md)中所述，注册中断服务例程（ISR）。

然后，在[*AVStrMiniDeviceStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicepnpstart)启动调度：

1.  使用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)设置 DMA 适配器对象。

2.  通过调用[**KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)，将 DMA 适配器对象注册到 AVStream。

微型驱动程序通过在对[**KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)的调用中提供*MaxMappingByteCount*参数来指定单个散点/集合映射的最大大小。

如果任何散点/集合映射超出了此最大大小，则 AVStream 会自动将映射拆分为多个散点/集合映射，每个映射的大小不能大于在*MaxMappingByteCount*中指定的大小。

还必须提供[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)回调例程。 驱动程序编写器应为此回调选择合适的功能。 例如，你可以执行以下操作：

1.  调用[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)。

2.  通过调用[**KsStreamPointerClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)克隆前导边缘。

3.  基于克隆的计划 DMA 硬件。

4.  调用[**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)或[**KsStreamPointerAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvance)来前进领先的边缘。

5.  根据需要对其他帧重复步骤2。

当硬件中断用于 DMA 完成时，内核将调用供应商以前注册的 ISR。 在 ISR 中，微型驱动程序对延迟的过程调用（DPC）进行排队。

DPC 应更新**DataUsed** ，并且可能会更新[**KSSTREAM\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的其他成员。 然后，DPC 可以调用[**KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)来删除克隆并释放关联的帧。

或者，如果只是部分帧完成，则 DPC 可能会前进克隆指针。 为此，请调用[**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)。

如果需要恢复处理，请调用[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)。

请注意，如果映射的长度小于一个物理页，则不能保证它驻留在单个物理页上。

 

 




