---
title: 将接收筛选器移到虚拟端口
description: 将接收筛选器移到虚拟端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4014604fe17abf363620d267bddeb3a64dbfc12
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248643"
---
# <a name="moving-a-receive-filter-to-a-virtual-port"></a>将接收筛选器移到虚拟端口


过量驱动程序 (OID 发出对象标识符) 设置 [oid \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md) ，以将接收筛选器从虚拟端口 (VPort) 移动到 NIC 交换机上的另一个 VPort。 通常情况下，如果满足以下任一条件，则会发出此 OID 请求的过量驱动程序，如虚拟化堆栈：

-   虚拟化堆栈设置默认 VPort 上的接收筛选器。 此筛选器包含 Hyper-v 子分区中公开的虚拟机 (VM) 网络适配器的媒体访问控制 (MAC) 地址和虚拟 LAN (VLAN) 参数。 这允许在 VM 网络适配器和基础网络适配器之间通过基于软件的合成数据路径转发数据包。

    在 PCI Express (PCIe 的资源) 虚函数 (分配了 VF) 并将 VF 附加到子分区后，虚拟化堆栈会在 VF 上创建一个非默认 VPort。 然后，虚拟化堆栈将 VM 网络适配器的接收筛选器从默认 VPort 移动到附加到 VF 的非默认的 VPort。 这允许数据包通过基于硬件的 VF 数据路径在 VM 网络适配器和基础网络适配器之间转发。

    有关这些数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

-   VF 与来宾操作系统仍在运行的 Hyper-v 子分区分离。 在这种情况下，过量驱动程序发出 OID set 请求，将 VM 网络适配器的接收筛选器从非默认 VPort 移动到附加到 PF 的默认 VPort。 发生这种情况时，数据包流量将恢复为合成数据路径。

若要将接收筛选器从一个 VPort 移到另一个 VPort，过量驱动程序将发出 Oid 请求，即 [oid \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md)。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构的指针。

在过量驱动程序发出 [OID \_ 接收筛选 \_ 器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md) 请求之前，它必须按以下方式初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters) 结构：

-   驱动程序将 **FilterId** 成员设置为先前分配的接收筛选器的标识符的标识符。

    **注意**  过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器或 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选](./oid-receive-filter-enum-filters.md)器的早期 OID 方法请求中获取了筛选器标识符。

     

-   驱动程序将 **SourceQueueId** 成员设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   驱动程序将 **SourceVPortId** 成员设置为之前设置此筛选器的 VPort 的标识符。

-   驱动程序将 **DestQueueId** 成员设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   驱动程序将 **DestVPortId** 成员设置为要将此筛选器移动到的 VPort 的标识符。

NDIS 验证 [**ndis 接收筛选器的 \_ 成员 \_ \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters) ，然后将 OID 集请求转发到 PF 微型端口驱动程序。

当 PF 微型端口驱动程序处理此 OID 集请求时，它必须在原子操作中移动接收筛选器。 驱动程序必须能够将网络适配器配置为同时从接收队列和 VPort 中删除筛选器，并将其设置在不同的接收队列和 VPort 中。

 

