---
title: Storport 驱动程序
description: Storport 驱动程序
ms.assetid: d5bda2f6-c4bb-4b90-a149-131785295687
keywords:
- 存储端口驱动程序 WDK、 Storport 驱动程序
- Storport 驱动程序 WDK
- Storport 驱动程序 WDK，有关 Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75eec4c3bcd6edc2b1b95de2832c84ed03a474cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565134"
---
# <a name="storport-driver"></a>Storport 驱动程序


## <span id="ddk_storport_driver_kg"></span><span id="DDK_STORPORT_DRIVER_KG"></span>


SCSI 端口驱动程序，除了 Microsoft Windows Server 2003 及更高版本提供 Storport (*storport.sys*)，尤其是适用于高性能总线，例如光纤通道的存储端口驱动程序总线和 RAID 适配器。

有以下几个使用 SCSI 端口驱动程序而不 Storport 优点：

-   改进了的性能，吞吐量和系统资源正在使用的两个方面。

-   改进的微型端口驱动程序接口地址的需求的高端存储供应商，尤其是基于主机的 RAID 和光纤通道供应商。

所有供应商是建议在可能的情况下，使用 Storport 而不是 SCSI 端口驱动程序。 存在一些限制，但是。 Storport 不能用于适配器或不支持即插的设备。 因为 Storport 不支持对编程 I/O 或从属模式 DMA，总线主控 DMA 功能，必须拥有 DMA 的所有设备。 从带标记的队列 autorequest 意义上，WMI 支持，设备必须报告的 SCSI 查询数据的排序和直接从适配器的 ROM BIOS 启动应用其他限制。 Storport 驱动程序的使用限制的详细列表，请参阅[要求与适配器使用 Storport](requirements-for-using-storport-with-an-adapter.md)。

若要更好地利用供应商 SCSI 端口微型端口驱动程序中所做的投资，Storport 遵循了 SCSI 端口微型端口驱动程序体系结构以及少量修改。 新的算法已能够生成可衡量的速度会增加，或已添加对高速总线支持所需几个方面进行了更改到 SCSI 端口驱动程序接口。

本部分包括以下主题：

[Storport 驱动程序的生命周期](life-cycle-of-a-storport-driver.md)

[Storport 的历史记录](history-of-storport.md)

[所提供的 Storport 功能](capabilities-provided-by-storport.md)

[Storport 的存储类驱动程序接口](storport-s-interface-with-the-storage-class-driver.md)

[Storport 的接口与 Storport 微型端口驱动程序](storport-s-interface-with-storport-miniport-drivers.md)

[Storport I/O 模型](storport-i-o-model.md)

[Storport 队列管理](storport-queue-management.md)

[Storport 事件日志扩展](storport-event-log-extensions.md)

[Storport 错误管理](storport-error-management.md)

[Storport 空闲电源管理](storport-idle-power-management.md)

[Storport 制定 SCSI 端口微型端口驱动程序处理](making-scsi-port-miniport-drivers-work-with-storport.md)

 

 




