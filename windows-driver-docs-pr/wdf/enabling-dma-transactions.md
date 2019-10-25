---
title: 启用 DMA 事务
description: 启用 DMA 事务
ms.assetid: 87735776-c371-425b-bc53-0c68375c9562
keywords:
- DMA 事务 WDK KMDF，启用
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e507648cd48cddbdfc8dfcded0e9bad9b10eca1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842856"
---
# <a name="enabling-dma-transactions"></a>启用 DMA 事务


\[仅适用于 KMDF\]




如果基于框架的驱动程序处理 DMA 设备的 i/o 操作，则驱动程序必须为每个 DMA 设备启用框架的 DMA 功能。 若要启用这些功能，驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)或[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数必须：

1.  调用[**WdfDeviceSetAlignmentRequirement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)以指定设备对缓冲区对齐的要求。

2.  调用[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)可指定 DMA 操作的类型（单数据包或分散/收集）以及设备支持的最大传输大小。 从 KMDF 版本1.11 开始，框架支持在 Windows 8 或更高版本的操作系统上运行的基于芯片（SoC）系统上的系统[模式下的 DMA](supporting-system-mode-dma.md) 。

3.  如果设备支持分散/收集操作，请调用[**WdfDmaEnablerSetMaximumScatterGatherElements**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablersetmaximumscattergatherelements)以指定设备可在散点/集合列表中支持的最大元素数。

[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例中的以下代码示例演示了如何启用框架的 DMA 功能。 此代码出现在*Init .c 文件*中。

```cpp
WDF_DMA_ENABLER_CONFIG   dmaConfig;

WdfDeviceSetAlignmentRequirement( DevExt->Device, PCI9656_DTE_ALIGNMENT_16 );
WDF_DMA_ENABLER_CONFIG_INIT( &dmaConfig,
                             WdfDmaProfileScatterGather64Duplex,
                             DevExt->MaximumTransferLength );
status = WdfDmaEnablerCreate( DevExt->Device,
                              &dmaConfig, 
                              WDF_NO_OBJECT_ATTRIBUTES,
                              &DevExt->DmaEnabler );
```

如果驱动程序需要公用缓冲区，则驱动程序的*EvtDriverDeviceAdd*回调函数通常会设置它们。 有关这些缓冲区的详细信息，请参阅[使用公用缓冲区](using-common-buffers.md)。

当驱动程序调用**WdfDmaEnablerCreate**后，它可以调用[**WdfDmaEnablerWdmGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)来获取指向 WDM [**DMA\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)结构的指针，该类型是框架为设备的输入和输出方向创建的。 但是，大多数基于框架的驱动程序不需要访问这些结构。









