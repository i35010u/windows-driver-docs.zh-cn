---
title: 分配 VM 队列
description: 分配 VM 队列
ms.assetid: 2645a6e5-3824-469c-84d5-8e49fa01f494
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a1d0fec4665ac6c690687f62530f37d3cc9764
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835390"
---
# <a name="allocating-a-vm-queue"></a>分配 VM 队列





如果要使用一组初始配置参数分配队列，则过量驱动程序会发出[OID\_接收\_FILTER\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)方法 OID 请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。 成功从 OID 方法请求返回后， **ndis\_OID\_请求**结构包含一个指向**ndis\_接收\_\_队列**的指针，该指针包含一个新队列标识符和一个 MSI-X 表项。

[**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构用于[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)OID 和[OID\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)\_\_\_ 有关 VM 队列参数的详细信息，请参阅[获取和更新 Vm 队列参数](obtaining-and-updating-vm-queue-parameters.md)。

上层驱动程序初始化[**NDIS\_接收\_queue\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，并具有以下队列配置参数：

-   队列类型（**NdisReceiveQueueTypeVMQueue**从[**NDIS\_接收\_队列\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_queue_type)枚举。）

-   队列的处理器关联。

-   队列名称和虚拟机名称。

-   预测先行-拆分参数。

    **请注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。

     

**请注意**  过量驱动程序可以设置 NDIS\_接收\_队列\_参数\_每个\_队列\_接收\_指示，NDIS\_接收\_队列\_参数\_\_\_\_\_[**参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**FLAGS**成员中拆分\_必需的标志。 其他标志不用于队列分配。

 

当 NDIS 接收到分配接收队列的 OID 请求时，它将验证队列参数。 在 NDIS 分配所需的资源和队列标识符后，它会将 OID 请求提交到基础微型端口驱动程序。 队列标识符对于关联的网络适配器是唯一的。

如果微型端口驱动程序可以成功分配接收队列所需的软件和硬件资源，则它将以成功状态完成 OID 请求。

在 NDIS 将 OID 请求发送到微型端口驱动程序之前，NDIS [ **\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构，并将方法请求传递给微型端口驱动程序，在 Ndis 的**QueueId**成员中分配队列标识符。 微型端口驱动程序在**MSIXTableEntry**成员中提供了 MSI-X 表条目。

微型端口驱动程序必须保留已分配接收队列的队列标识符。 对于对微型端口驱动程序的后续调用，NDIS 使用接收队列的队列标识符来设置接收队列的接收筛选器、更改接收队列参数或释放接收队列。

**请注意**  默认队列（队列标识符为零）始终被分配，并且无法释放。

 

过量驱动程序必须使用 NDIS 在后续 OID 请求中提供的队列标识符，例如，修改队列参数或释放队列。 队列标识符也包含在所有[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的 OOB 数据中\_与该队列关联的列表结构。 驱动程序使用[**net\_BUFFER\_列表\_接收\_队列\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)宏，以检索 NET\_缓冲区\_列表结构中的队列标识符。

**请注意**  协议驱动程序在成功分配了队列之后以及在删除队列之前，可以随时设置 VMQ 筛选器。

 

协议驱动程序发出[OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)方法 OID 请求来完成队列分配。 小型端口驱动程序可以在分配完成时分配共享内存和其他资源。 有关分配共享内存资源的详细信息，请参阅[共享内存资源分配](shared-memory-resource-allocation.md)。

在微型端口驱动程序接收 OID 后\_接收\_筛选器\_队列\_分配 OID 请求并成功处理该请求，队列处于已*分配*状态。 有关队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

在覆盖后的驱动程序分配一个或多个接收队列（并且可以选择设置初始筛选器）后，它必须[\_筛选\_器发出 OID\_接收筛选器\_分配\_完整](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)的设置 OID 请求，通知微型端口驱动程序分配已完成，当前批次接收队列。

如果没有对该队列设置任何筛选器，则微型端口驱动程序不得保留接收队列中的任何数据包。 如果队列从未设置任何筛选器或清除了所有筛选器，则队列应为空，并且应丢弃所有数据包。 也就是说，它们不会显示在驱动程序堆栈上，也不会保留在队列中。

过量驱动程序使用[OID\_接收\_筛选器\_可用的\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)OID，以释放它们分配的队列。 有关释放队列的详细信息，请参阅[释放 VM 队列](freeing-a-vm-queue.md)。

 

 





