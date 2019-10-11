---
title: Storport 驱动程序
description: Storport 驱动程序
ms.assetid: d5bda2f6-c4bb-4b90-a149-131785295687
keywords:
- 存储端口驱动程序 WDK、Storport 驱动程序
- Storport 驱动程序 WDK
- Storport 驱动程序 WDK，关于 Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75eec4c3bcd6edc2b1b95de2832c84ed03a474cb
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72271822"
---
# <a name="storport-driver"></a>Storport 驱动程序


## <span id="ddk_storport_driver_kg"></span><span id="DDK_STORPORT_DRIVER_KG"></span>


除了 SCSI 端口驱动程序以外，Microsoft Windows Server 2003 和更高版本还提供 Storport （*storport*），这是一个特别适用于高性能总线（如光纤通道总线和 RAID 适配器）的存储端口驱动程序。

使用 Storport （而非 SCSI 端口驱动程序）有以下几个优点：

-   提高了性能，包括吞吐量和使用的系统资源。

-   提高了微型端口驱动程序接口，可满足高端存储供应商的需求，尤其是基于主机的 RAID 和光纤通道供应商。

建议所有供应商尽可能使用 Storport，而不是 SCSI 端口驱动程序。 但会应用某些限制。 Storport 不能与不支持即插即用的适配器或设备一起使用。 所有 DMA 设备都必须具有总线控制 DMA 功能，因为 Storport 不支持程控 i/o 或从属模式 DMA。 其他限制适用于标记队列、autorequest 感知、WMI 支持、设备必须报告的 SCSI 查询数据的种类以及直接从适配器的 ROM BIOS 启动的情况。 有关使用 Storport 驱动程序的详细限制列表，请参阅对[适配器使用 storport 的要求](requirements-for-using-storport-with-an-adapter.md)。

为了更好地利用供应商在 SCSI 端口微型端口驱动程序中所做的投资，Storport 遵循 SCSI 端口-微型端口驱动程序体系结构，只需进行很少的修改。 对 SCSI 端口驱动程序接口的更改是在新算法能够产生可度量的速度增加的区域中进行的，或者是需要为高速总线添加支持的位置。

本部分包括以下主题：

[Storport 驱动程序的生命周期](life-cycle-of-a-storport-driver.md)

[Storport 历史记录](history-of-storport.md)

[Storport 提供的功能](capabilities-provided-by-storport.md)

[Storport 与存储类驱动程序的接口](storport-s-interface-with-the-storage-class-driver.md)

[Storport 与 Storport 微型端口驱动程序的接口](storport-s-interface-with-storport-miniport-drivers.md)

[Storport i/o 模型](storport-i-o-model.md)

[Storport 队列管理](storport-queue-management.md)

[Storport 事件日志扩展](storport-event-log-extensions.md)

[Storport 错误管理](storport-error-management.md)

[Storport 空闲电源管理](storport-idle-power-management.md)

[使 SCSI 端口微型端口驱动程序可用于 Storport](making-scsi-port-miniport-drivers-work-with-storport.md)

 

 




