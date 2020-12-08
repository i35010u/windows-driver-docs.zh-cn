---
title: 启用 DMA 事务
description: 启用 DMA 事务
keywords:
- DMA 事务 WDK KMDF，启用
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4a5a0b9fbfb979ee19284df44597145ff781854
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815767"
---
# <a name="enabling-dma-transactions"></a>启用 DMA 事务


\[仅适用于 KMDF\]




如果基于框架的驱动程序处理 DMA 设备的 i/o 操作，则驱动程序必须为每个 DMA 设备启用框架的 DMA 功能。 若要启用这些功能，驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 或 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数必须：

1.  调用 [**WdfDeviceSetAlignmentRequirement**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement) 以指定设备对缓冲区对齐的要求。

2.  调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) 指定 DMA 操作的类型 (单包或分散/收集) ，以及设备支持的最大传输大小。 从 KMDF 版本1.11 开始，该框架支持在 Windows 8 或更高版本的操作系统上运行的基于芯片 (SoC) 系统上的系统上的 [系统模式 DMA](supporting-system-mode-dma.md) 。

3.  如果设备支持分散/收集操作，请调用 [**WdfDmaEnablerSetMaximumScatterGatherElements**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablersetmaximumscattergatherelements) 以指定设备可在散点/集合列表中支持的最大元素数。

[PLX9x5x](/samples/browse/)示例中的以下代码示例演示了如何启用框架的 DMA 功能。 此代码出现在 *Init .c 文件* 中。

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

如果驱动程序需要公用缓冲区，则驱动程序的 *EvtDriverDeviceAdd* 回调函数通常会设置它们。 有关这些缓冲区的详细信息，请参阅 [使用公用缓冲区](using-common-buffers.md)。

当驱动程序调用 **WdfDmaEnablerCreate** 后，它可以调用 [**WdfDmaEnablerWdmGetDmaAdapter**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter) 来获取对该框架为设备的输入和输出方向创建的 WDM [**DMA \_ 适配器**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter) 结构的指针。 但是，大多数基于框架的驱动程序不需要访问这些结构。
