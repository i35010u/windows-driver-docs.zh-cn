---
title: 分配 VM 队列
description: 分配 VM 队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e64e45977e921e169aa098448c57c802cd8bf10
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247774"
---
# <a name="allocating-a-vm-queue"></a>分配 VM 队列





如果要使用一组初始配置参数分配队列，则过量驱动程序会发出 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) 方法 oid 请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。 成功从 OID 方法请求返回后， **ndis \_ OID \_ 请求** 结构的 **InformationBuffer** 成员包含指向 **ndis \_ 接收 \_ 队列 \_ 参数** 结构的指针，该结构具有新的队列标识符和一个 MSI-X 表项。

在 [oid 接收 \_ \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md)OID 和 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](./oid-receive-filter-queue-parameters.md)OID 中使用 [**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构。 有关 VM 队列参数的详细信息，请参阅 [获取和更新 Vm 队列参数](obtaining-and-updating-vm-queue-parameters.md)。

上层驱动程序用以下队列配置参数初始化 [**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters) 结构：

-   从 [**NDIS \_ 接收 \_ 队列 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_queue_type)枚举 (**NdisReceiveQueueTypeVMQueue** 的队列类型。 ) 

-   队列的处理器关联。

-   队列名称和虚拟机名称。

-   预测先行-拆分参数。

    **注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。

     

**注意** 过量驱动程序可以在 Ndis 接收 \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ [**\_ \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的 **flags** 成员中设置每个队列接收指示和 ndis 接收队列参数的 ndis 接收队列参数。 其他标志不用于队列分配。

 

当 NDIS 接收到分配接收队列的 OID 请求时，它将验证队列参数。 在 NDIS 分配所需的资源和队列标识符后，它会将 OID 请求提交到基础微型端口驱动程序。 队列标识符对于关联的网络适配器是唯一的。

如果微型端口驱动程序可以成功分配接收队列所需的软件和硬件资源，则它将以成功状态完成 OID 请求。

在 NDIS 向微型端口驱动程序发送 OID 请求之前，NDIS 在 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的 **QueueId** 成员中分配一个队列标识符，并将该方法请求传递给微型端口驱动程序。 微型端口驱动程序在 **MSIXTableEntry** 成员中提供了 MSI-X 表条目。

微型端口驱动程序必须保留已分配接收队列的队列标识符。 对于对微型端口驱动程序的后续调用，NDIS 使用接收队列的队列标识符来设置接收队列的接收筛选器、更改接收队列参数或释放接收队列。

**注意**  默认队列 (队列标识符 0) 始终被分配，无法释放。

 

过量驱动程序必须使用 NDIS 在后续 OID 请求中提供的队列标识符，例如，修改队列参数或释放队列。 队列标识符也包含在与队列关联的所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构上的 OOB 数据中。 驱动程序使用 [**网络 \_ 缓冲区 \_ 列表 \_ 接收 \_ 队列 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_queue_id) 宏来检索网络 \_ 缓冲区列表结构中的队列标识符 \_ 。

**注意**  协议驱动程序可以在成功分配队列后、删除队列之前随时设置 VMQ 筛选器。

 

协议驱动程序发出 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) 方法 oid 请求，以完成队列分配。 小型端口驱动程序可以在分配完成时分配共享内存和其他资源。 有关分配共享内存资源的详细信息，请参阅 [共享内存资源分配](shared-memory-resource-allocation.md)。

当微型端口驱动程序收到 OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 oid 请求并成功处理该请求后，该队列将处于已 *分配* 状态。 有关队列状态的详细信息，请参阅 [队列状态和操作](queue-states-and-operations.md)。

当过量驱动程序分配一个或多个接收队列 (并根据需要将初始筛选器设置) 时，它必须发出 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) set OID 请求，通知微型端口驱动程序已为当前批次接收队列分配完成。

如果没有对该队列设置任何筛选器，则微型端口驱动程序不得保留接收队列中的任何数据包。 如果队列从未设置任何筛选器或清除了所有筛选器，则队列应为空，并且应丢弃所有数据包。 也就是说，它们不会显示在驱动程序堆栈上，也不会保留在队列中。

过量驱动程序使用 [oid \_ 接收 \_ 筛选器 \_ 免费 \_ 队列](./oid-receive-filter-free-queue.md) OID 来释放它们分配的队列。 有关释放队列的详细信息，请参阅 [释放 VM 队列](freeing-a-vm-queue.md)。

 

