---
title: 更改 MSI-X 表项的 CPU 关联
description: 更改 MSI-X 表项的 CPU 关联
keywords:
- MSI-X WDK 网络，MSI-X 表条目 CPU 相关性
- 消息-已发出信号中断 WDK 网络，MSI-X 表条目 CPU 相关性
- Msi WDK 网络，MSI-X 表条目 CPU 相关性
- 中断 WDK 网络，MSI-X 表条目 CPU 相关性
- CPU af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ece86105ceee964009a3413c58cab67a8e6b26c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787299"
---
# <a name="changing-the-cpu-affinity-of-msi-x-table-entries"></a>更改 MSI-X 表项的 CPU 关联





支持 MSI X 的 NDIS 6.1 和更高版本的小型小型驱动程序可以调用 [**NdisMConfigMSIXTableEntry**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry) 函数来屏蔽、取消屏蔽或将 Msi-x 表项映射到设备分配的 msi x 消息。 支持 RSS 的微型端口驱动程序在运行时使用 **NdisMConfigMSIXTableEntry** 更改 MSI-X 表项的 CPU 关联。

**NdisMConfigMSIXTableEntry** 是 [GUID \_ .msix \_ 表 \_ 配置 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/ff546563) 查询周围的包装器。 当 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数并在驱动程序从 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数返回之前，微型端口驱动程序可以调用 **NdisMConfigMSIXTableEntry** 。

一种微型端口驱动程序，它为每个 RSS 队列分配一个 MSI-X 表条目，并且该驱动程序的队列数少于 RSS 处理器数量，可以在 [*MiniportFilterResourceRequirements*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp) 函数中添加其他的 msi x 消息资源。 有关如何修改设备的已分配资源的详细信息，请参阅 [MSI-X 资源筛选](msi-x-resource-filtering.md)。

微型端口驱动程序可以设置 MSI X 中断资源的 CPU 关联，使每个 RSS 处理器的设备至少具有一个 hyper-v 消息。 请注意，PCI 总线驱动程序最初会映射 *n* 个 Msi-x 表条目 (其中 *n* 是 NIC 硬件报告给总线的 msi-x 表条目数) 到修改后的资源中的前 *n* 个 msi x 消息。 在 NDIS 调用 *MiniportInitializeEx* 后，当微型端口驱动程序更改特定的 MSI-x 表条目的目标处理器时，驱动程序将调用 **NdisMConfigMSIXTableEntry** 将该表项映射到已将关联设置为所需处理器的 MSI X 消息。

 

