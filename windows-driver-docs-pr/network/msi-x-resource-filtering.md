---
title: MSI-X 资源筛选
description: MSI-X 资源筛选
ms.assetid: ccc6aac0-7c89-4e48-ac53-9e3a72965a43
keywords:
- MSI-X WDK 网络，资源需求筛选器函数
- 消息-已发出信号中断 WDK 网络，资源需求筛选器函数
- Msi WDK 网络，资源需求筛选器函数
- 资源需求筛选器函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01efd6bc1d50d37ebae7a9a1f90d8ce55dde608f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844212"
---
# <a name="msi-x-resource-filtering"></a>MSI-X 资源筛选





微型端口驱动程序必须注册资源需求筛选器函数，前提是它们支持 MSI X，将更改每个 MSI X 消息的中断相关性，或将删除消息中断资源。

Ndis 在 NDIS 接收[**IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)用于网络接口卡（NIC）的 i/o 请求数据包（IRP）后，调用[*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)函数。 在设备堆栈中的基础函数驱动程序完成 IRP 后，NDIS 将调用*MiniportFilterResourceRequirements* 。

[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)函数\_SUCCESS 返回 NDIS\_状态之后，ndis 将调用*MiniportFilterResourceRequirements* 。 在调用[*MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)之前，NDIS 可随时再次调用*MiniportFilterResourceRequirements* 。 当微型端口正在运行时，NDIS 可以调用*MiniportFilterResourceRequirements* 。 当微型端口可以按如下所述修改资源列表时，微型端口不应该立即尝试使用新资源。 NDIS 最终将停止并重新初始化带新资源的小型端口;只有在微型端口尝试使用新资源时才应如此。

[**Irp\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)将资源列表提供为[**IO\_资源**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)列表\_资源**列表。** 此列表中的资源由[**IO\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)结构描述。

微型端口驱动程序可以修改**CmResourceTypeInterrupt**类型的每个资源的中断关联策略，这些资源描述了一个 MSI-X 消息。 如果关联策略请求特定处理器集的目标，则微型端口驱动程序还会在 IO\_资源\_描述符**结构中设置** [**KAFFINITY**](https://docs.microsoft.com/windows-hardware/drivers/kernel/interrupt-affinity-and-priority#about-kaffinity)掩码。

微型端口驱动程序可以删除作为消息中断资源的**CmResourceTypeInterrupt**类型的所有资源。 然后，驱动程序可以在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数中注册基于行的中断。 如果微型端口驱动程序未删除这些消息中断资源，则当驱动程序尝试在*MiniportInitializeEx*中注册基于行的中断时，操作系统将会失败。

NDIS 6.1 或更高版本的微型端口驱动程序可以将消息中断资源添加到资源列表。 例如，在具有8个 Cpu 的计算机上，如果 NIC 可以生成四个 MSI X 消息，并且如果操作系统启用四个消息中断，则操作系统会在设备的 MSI X 配置空间中初始化四个消息表项，并将四个资源列表中的消息中断资源。 在这种情况下，由于微型端口驱动程序需要更多的消息中断资源，因此它可以向 resources 列表分配另外四个消息中断资源，并将每个 MSI X 消息的相关性设置为 CPU。 如果操作系统可以提供更多的消息中断资源，微型端口适配器将在启动时收到8个消息中断资源。 在这种情况下，消息具有0到7之间的数字。

列表中的每个消息中断资源将在后面分配一个与它在列表中显示的顺序相对应的消息号。 例如，列表中的第一条消息中断资源分配给消息0，第二个资源分配给消息1，依此类推。

若要在运行时向 CPU 分配一个 MSI-X 表项，微型端口驱动程序可以调用[**NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry)函数，该函数将一个表条目映射到已将关联设置为 CPU 的 MSI X 消息。 有关 MSI-X 表项的配置操作的详细信息，请参阅[更改 msi-x 表项的 CPU 关联](changing-the-cpu-affinity-of-msi-x-table-entries.md)。

若要为新的资源需求列表分配内存，请使用[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)函数。 可以通过[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)函数释放旧资源需求列表的内存。

微型端口驱动程序不应修改其他资源，如**CmResourceTypeMemory**和**CmResourceTypePort**资源。 微型端口驱动程序应避免将新资源添加到资源列表。 但是，NDIS 6.1 和更高版本的微型端口驱动程序可以添加更多的消息中断资源。 如果微型端口驱动程序添加了更多的消息中断资源，则不能将其从[*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)函数中删除。

有关添加和删除资源的详细信息，请参阅[**IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)。

