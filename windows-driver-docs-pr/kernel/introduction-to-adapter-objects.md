---
title: 适配器对象简介
description: 适配器对象简介
keywords:
- AdapterControl 例程，关于 AdapterControl 例程
- DMA 传输 WDK 内核，适配器对象
- 适配器对象 WDK 内核，关于适配器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50397fdffac0326a54d0372acea1c743dea7a857
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815277"
---
# <a name="introduction-to-adapter-objects"></a>适配器对象简介





使用直接 i/o 和 DMA 的任何驱动程序都必须创建一个适配器对象。 适配器对象表示 DMA 控制器通道或端口，或者是主线主机设备。

两种最低级别的驱动程序必须使用适配器对象：

-   使用系统 DMA 控制器的设备驱动程序。 此类设备称为 *从属设备* ，称为 "使用系统 (或 *从属*) DMA"。

-   作为总线-主适配器的设备的驱动程序。 此类设备会使用系统进行仲裁，以使用 i/o 总线，因此使用的是总线主控 DMA。

驱动程序为指向适配器对象的指针提供存储，通常在设备扩展中。

若要执行 DMA 传输，使用这两种 DMA 方法的设备的驱动程序通常具有 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程，并调用系统提供的支持例程来处理适配器对象。 不需要 *AdapterControl* 例程的 (驱动程序包括那些 [使用散播/聚集 Dma](using-scatter-gather-dma.md) 的驱动程序，以及 [使用常见缓冲区、总线主 dma](using-common-buffer-bus-master-dma.md)的驱动程序。 ) 

作为设备启动操作的一部分，处理 DMA 操作的驱动程序调用 i/o 管理器，该管理器反过来调用特定于平台的 HAL 来创建一组适配器对象。 在任何 Windows 平台上，适配器对象集通常包含用于的适配器对象：

-   从属设备连接到的每个系统 DMA 控制器通道或端口。

-   计算机中的每个主线主机 DMA 设备。

 (适用于支持总线主机 DMA 的 SCSI 设备，SCSI 端口驱动程序为特定于 HBA 的 SCSI 微型端口驱动程序设置适配器对象。 微型端口驱动程序的 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 例程为端口驱动程序提供特定于适配器的数据。 ) 

若要详细了解何时以及如何使用适配器对象和 *AdapterControl* 例程，请参阅此部分以及 [使用 Bus-Master DMA](using-bus-master-dma.md) 。

## <a name="related-topics"></a>相关主题

[为设备驱动程序启用 DMA 重新映射](../pci/enabling-dma-remapping-for-device-drivers.md)

 

