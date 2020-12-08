---
title: 使用中断资源描述符
description: 使用中断资源描述符
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 263f66885c01ed378c13a4f1ddf046bdc50ada7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793491"
---
# <a name="using-interrupt-resource-descriptors"></a>使用中断资源描述符


即插即用 (PnP) 管理器使用两个传递向设备分配中断消息。 首先，PnP 管理器将 [**IRP \_ MN \_ FILTER \_ 资源 \_ 需求**](./irp-mn-filter-resource-requirements.md) 请求发送到驱动程序，其中包含要分配给设备的硬件资源（包括中断消息）的列表。 驱动程序可以修改此列表以更改中断消息的数目以及某些每个消息的设置。 然后，在 PnP 管理器实际分配资源之后，它将发送 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求，并提供分配给驱动程序的设备的硬件资源的完整列表，包括中断消息。

**IRP \_ MN \_ FILTER \_ 资源 \_ 需求** 请求提供 [**IO \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)结构的列表。 如果设备具有在 PCI 2.2 规范中定义的 MSI (消息已发出中断) 功能结构，则 PnP 管理器会提供单个中断消息描述符。 如果设备具有 PCI 3.0 规范中定义的 MSI X 功能结构，则 PnP 管理器为每个中断消息提供一个结构。 中断消息描述符的 **类型**  =  为 **CmResourceTypeInterrupt** ，**标志**= CM \_ 资源 \_ 中断 \_ 锁定 |CM \_ 资源 \_ 中断 \_ 消息。 驱动程序还可以通过更改结构的 " **u** " 成员来更改设置，如中断相关性。 请注意，使用 MSI 时，中断都具有相同的关联，而使用 MSI X 时，它们可以具有不同的相关性。 有关详细信息，请参阅 [中断相关性和优先级](interrupt-affinity-and-priority.md)。

对于在 PCI 2.2 中定义的 MSI， **MaximumVector**  -  **MinimumVector** + 1 是为设备分配的中断消息的数目。 驱动程序可以通过修改 **MinimumVector** 更改中断消息的数量。 对于 MSI 中断消息， **MaximumVector** 始终是 CM \_ 资源 \_ 中断 \_ 消息 \_ 标记。 若要分配 *MessageCount* 中断消息，请将 **MinimumVector** 设置为等于 CM \_ 资源 \_ 中断 \_ 消息 \_ 令牌- *MessageCount* + 1。

对于在 PCI 3.0 中定义的 MSI-X，驱动程序可以通过添加或删除列表中的条目来更改分配的中断消息的数量。 请注意，为了响应 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求，无法随后删除以这种方式添加的中断消息资源。 对于 MSI X，PnP 管理器为每个消息中断提供一个描述符，并将此描述符的 **MinimumVector** 和 **MaximumVector** 成员设置为 CM \_ 资源 \_ 中断 \_ 消息 \_ 标记。

即插即用管理器分配了设备的所有硬件资源（包括中断消息）后，它会将 **IRP \_ MN \_ 启动 \_ 设备** 请求发送到该驱动程序。 此请求提供两个 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor) 结构列表，每个列表用于原始资源和已转换资源。 对于中断消息，PnP 管理器为每个分配的内存地址提供一个结构，其 **类型** 为  =  **CmResourceTypeInterrupt** ，**标志**= CM \_ 资源 \_ 中断 \_ 锁定 |CM \_ 资源 \_ 中断 \_ 消息。

请注意，使用 MSI 时，驱动程序只接收一个中断资源描述符，因为所有消息共享同一地址。 **MessageInterrupt** 的 **MessageCount** 成员可用于确定所分配的消息数。 使用 MSI X 时，驱动程序将为每个中断消息收到单独的资源描述符。

在 Windows 8 中，操作系统不支持每个设备的每个设备运行超过2048个中断消息的资源请求。 在 Windows 7 和 Windows Vista 中，操作系统不支持对每个设备的每个设备运行超过910个中断消息的资源请求。 如果设备驱动程序超过此限制，则设备可能无法启动。 若要使驱动程序在包含多个逻辑处理器的计算机上运行，该驱动程序应避免为每个处理器请求多个中断。

在系统重新平衡中断资源的过程中，PnP 管理器可能会要求驱动程序从资源需求列表中选择首选的备用中断资源集。 但是，PnP 管理器不能始终向驱动程序分配驱动程序首选的资源。 因此，该驱动程序必须在不出现故障的情况下允许从资源需求列表分配任何备用中断资源集。 例如，可能会为设备分配比请求的驱动程序数更少的消息中断。 在最坏的情况下，驱动程序必须准备好只需一个基于线路的中断即可操作设备。

 

