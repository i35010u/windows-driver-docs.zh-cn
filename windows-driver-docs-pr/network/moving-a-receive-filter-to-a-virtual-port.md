---
title: 将接收筛选器移到虚拟端口
description: 将接收筛选器移到虚拟端口
ms.assetid: 6315FB18-3F57-43C2-B864-3759058092BB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28616bdb1c4519289af795b7dc780a24a888e68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844218"
---
# <a name="moving-a-receive-filter-to-a-virtual-port"></a>将接收筛选器移到虚拟端口


过量驱动程序发出[OID\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)的对象标识符（oid）设置请求，\_MOVE\_FILTER 将接收筛选器从虚拟端口（VPort）移动到 NIC 交换机上的另一个 VPort。 通常情况下，如果满足以下任一条件，则会发出此 OID 请求的过量驱动程序，如虚拟化堆栈：

-   虚拟化堆栈设置默认 VPort 上的接收筛选器。 此筛选器包含 Hyper-v 子分区中公开的虚拟机（VM）网络适配器的媒体访问控制（MAC）地址和虚拟 LAN （VLAN）参数。 这允许在 VM 网络适配器和基础网络适配器之间通过基于软件的合成数据路径转发数据包。

    为 PCI Express （PCIe）虚拟功能（VF）分配资源并将 VF 附加到子分区后，虚拟化堆栈会在 VF 上创建一个非默认的 VPort。 然后，虚拟化堆栈将 VM 网络适配器的接收筛选器从默认 VPort 移动到附加到 VF 的非默认的 VPort。 这允许数据包通过基于硬件的 VF 数据路径在 VM 网络适配器和基础网络适配器之间转发。

    有关这些数据路径的详细信息，请参阅[Sr-iov 数据路径](sr-iov-data-paths.md)。

-   VF 与来宾操作系统仍在运行的 Hyper-v 子分区分离。 在这种情况下，过量驱动程序发出 OID set 请求，将 VM 网络适配器的接收筛选器从非默认 VPort 移动到附加到 PF 的默认 VPort。 发生这种情况时，数据包流量将恢复为合成数据路径。

若要将接收筛选器从一个 VPort 移到另一个 VPort，则过量驱动程序会发出 oid 的 oid 集请求， [\_接收\_filter\_move\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)的指针\_\_参数结构移动\_筛选器。

在过量驱动程序发出[OID\_接收\_FILTER\_MOVE\_filter](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)请求之前，它必须\_[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)结构：

-   驱动程序将**FilterId**成员设置为先前分配的接收筛选器的标识符的标识符。

    **请注意**  过量驱动程序从 oid 的早期 oid 方法请求中获取了筛选器标识符[\_接收\_筛选器\_设置\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)器或 OID\_\_[枚举接收\_筛选器\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。

     

-   驱动程序将**SourceQueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

-   驱动程序将**SourceVPortId**成员设置为之前设置此筛选器的 VPort 的标识符。

-   驱动程序将**DestQueueId**成员设置为 NDIS\_默认\_接收\_队列\_ID。

-   驱动程序将**DestVPortId**成员设置为要将此筛选器移动到的 VPort 的标识符。

NDIS 验证[**ndis\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)的成员\_在将 OID 集请求转发到 PF 微型端口驱动程序之前，\_筛选器\_参数。

当 PF 微型端口驱动程序处理此 OID 集请求时，它必须在原子操作中移动接收筛选器。 驱动程序必须能够将网络适配器配置为同时从接收队列和 VPort 中删除筛选器，并将其设置在不同的接收队列和 VPort 中。

 

 





