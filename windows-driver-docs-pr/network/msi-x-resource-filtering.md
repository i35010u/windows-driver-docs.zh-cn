---
title: MSI-X 资源筛选
description: MSI-X 资源筛选
ms.assetid: ccc6aac0-7c89-4e48-ac53-9e3a72965a43
keywords:
- MSI X WDK 网络、 资源要求 filter 函数
- 消息信号中断 WDK 网络资源要求筛选器函数
- Msi WDK 网络资源要求筛选器函数
- 资源要求 filter 函数 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e18dc5708f0e36b58092e464340391bc7dab85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577348"
---
# <a name="msi-x-resource-filtering"></a>MSI-X 资源筛选





微型端口驱动程序必须注册资源要求筛选器函数，如果它们支持 MSI X，以及将更改为每个 MSI X 消息中断关联，或将删除消息中断资源。

NDIS 调用[ *MiniportFilterResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff559384) NDIS 接收后正常[ **IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874) I/O 请求数据包 (IRP) 网络接口卡 (NIC)。 NDIS 调用*MiniportFilterResourceRequirements*基础功能设备堆栈中的驱动程序已完成 IRP 后。

将调用 NDIS *MiniportFilterResourceRequirements*后[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)函数返回 NDIS\_状态\_成功。 可以调用 NDIS *MiniportFilterResourceRequirements*再次在调用前，随时[ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)。 可以调用 NDIS *MiniportFilterResourceRequirements*微型端口正在运行时。 虽然微型端口可以修改资源的列表，如下所述，微型端口不应立即尝试使用新的资源。 NDIS 最终将停止并重新初始化的新资源; 微型端口只有这样应微型端口尝试使用新的资源。

[**IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874)提供资源列表作为[ **IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)结构，在**Irp-&gt;IoStatus.Information**。 在列表中的资源均由描述[ **IO\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff550598)结构。

微型端口驱动程序可以修改每个资源类型的中断关联策略**CmResourceTypeInterrupt**描述 MSI X 消息。 如果关联策略请求特定的目标集的处理器，微型端口驱动程序还设置[ **KAFFINITY** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/interrupt-affinity-and-priority#about-kaffinity)在屏蔽**Interrupt.TargetedProcessors**中IO\_资源\_描述符结构。

微型端口驱动程序可删除所有资源类型的**CmResourceTypeInterrupt**是消息中断资源。 然后，驱动程序可以注册为在基于行的中断[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 如果微型端口驱动程序不会删除这些消息中断资源，则尝试注册中基于行的中断时该驱动程序，操作系统将失败*MiniportInitializeEx*。

NDIS 6.1 或更高版本的微型端口驱动程序可以将消息中断资源添加到资源列表中。 例如的计算机上有八个 Cpu，如果 NIC 可以生成四条 MSI X 消息，并且操作系统启用四个消息中断，操作系统初始化设备的 MSI X 配置空间中的四个消息表条目并将四个放在资源列表中的消息中断资源。 在这种情况下，由于微型端口驱动程序需要更多消息中断资源，它可以分配四个详细消息中断的资源添加到资源列表和每个 MSI X 消息的关联设置为一个 CPU。 如果操作系统可以提供更多消息中断资源，微型端口适配器接收消息中断的八个资源，在启动时。 在这种情况下，消息具有从 0 到 7 的数字。

在列表中的每个消息中断资源分配给它在列表中显示的顺序消息更高版本相对应的数字。 例如，在列表中的第一个消息中断资源分配到消息，0，第二个分配消息 1，依次类推。

若要在运行时将 MSI X 表项分配给一个 CPU，微型端口驱动程序可以调用[ **NdisMConfigMSIXTableEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff563566)函数，它将表条目映射到已具有关联设置为 MSI X 消息CPU。 有关 MSI X 表项的配置操作的详细信息，请参阅[MSI X 表条目 CPU Affinity 更改](changing-the-cpu-affinity-of-msi-x-table-entries.md)。

若要分配新的资源要求列表的内存，请使用[ **NdisAllocateMemoryWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff561606)函数。 可以免费使用旧的资源要求列表的内存[ **NdisFreeMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562577)函数。

微型端口驱动程序不应修改其他资源，如**CmResourceTypeMemory**并**CmResourceTypePort**资源。 微型端口驱动程序应避免将新的资源添加到资源列表。 但是，NDIS 6.1 和更高版本的微型端口驱动程序可以添加更多消息中断资源。 如果微型端口驱动程序添加更多消息中断资源，它必须不删除从中[ *MiniportStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559452)函数。

有关添加和删除资源的详细信息，请参阅[ **IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874)。

