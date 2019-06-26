---
title: AVStream 中基于数据包的 DMA
description: AVStream 中基于数据包的 DMA
ms.assetid: 4246819e-d8d6-4302-9477-675ca181b1e3
keywords:
- AVStream WDK 硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 基于数据包的 DMA WDK AVStream
- 散播-聚集 DMA WDK AVStream
- 捕获缓冲区 WDK AVStream
- 缓冲区 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35938834d7122f955de864be1e0ad0a676cc4796
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370390"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream 中基于数据包的 DMA





你微型驱动程序将直接来自数据和写入数据直接以捕获用户模式下从接收的缓冲区时发生访问 (DMA) 数据包基于的直接内存。 [AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)在 Windows 驱动程序工具包示例演示了如何生成执行这种类型的 DMA AVStream 微型驱动程序。

若要实现基于数据包的 DMA 方案：

1.  指定 KSPIN\_标志\_生成\_中的映射**标志**的相关成员[ **KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 请注意，此标志只应由基础总线散播-聚集支持。

2.  注册中断服务例程 (ISR) 中所述[写入 AVStream 微型驱动程序硬件](writing-avstream-minidrivers-for-hardware.md)。

然后在[ *AVStrMiniDeviceStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdevicepnpstart)启动调度：

1.  使用 DMA 适配器对象设置[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)。

2.  DMA 适配器对象注册 AVStream 通过调用[ **KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdeviceregisteradapterobject)。

微型驱动程序指定单一散播-聚集映射的最大大小，从而*MaxMappingByteCount*调用中的参数[ **KsDeviceRegisterAdapterObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdeviceregisteradapterobject).

如果任何散播-聚集映射超过此最大大小，AVStream 自动将中断映射到多个分散/聚拢映射，其中每个值中指定的大小不大于*MaxMappingByteCount*。

你还必须提供[ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)回调例程。 驱动程序编写器应选择相应的功能，此回调。 作为一个示例中，可以执行以下操作：

1.  调用[ **KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)。

2.  通过调用克隆前沿[ **KsStreamPointerClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)。

3.  基于克隆的程序 DMA 硬件。

4.  调用[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)或[ **KsStreamPointerAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvance)转前沿。

5.  重复步骤 2 所需的其他框架中。

当硬件中断的 DMA 完成情况时，内核会调用供应商以前已注册 ISR。 在 ISR，微型驱动程序队列的延迟的过程调用 (DPC)。

应更新你 DPC **DataUsed**及可能的其他成员[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构。 然后调用 DPC 可能[ **KsStreamPointerDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)删除克隆并释放关联的帧。

或者，如果只完成帧的一部分 DPC 可以继续学习克隆指针。 若要执行此操作，调用[ **KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)。

如有必要继续处理，调用[ **KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattemptprocessing)。

请注意，是否映射不到一个物理页的长度，也不能保证驻留在单个物理页上。

 

 




