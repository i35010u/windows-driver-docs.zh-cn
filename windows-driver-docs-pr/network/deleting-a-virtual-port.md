---
title: 删除虚拟端口
description: 删除虚拟端口
ms.assetid: CBE7AC59-D878-44BA-8FE6-168EC17A2D67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 628bbc2877baaa56864fd085109c61e21cf4bf54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834928"
---
# <a name="deleting-a-virtual-port"></a>删除虚拟端口


过量驱动程序发出 OID\_NIC 的对象标识符（OID）设置请求[\_交换机\_delete\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除网络适配器的 NIC 交换机上的非默认虚拟端口（VPORT）。 过量驱动程序只能删除先前创建的 VPort，方法是\_开关\_NIC 发出 oid 方法请求， [\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_交换机\_DELETE\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构。

过量驱动程序（例如虚拟化堆栈）可以删除先前创建的非默认 VPort。 过量驱动程序通过\_\_NIC 发出 oid 方法请求， [\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)，来创建一个 VPort。

在发出 oid\_NIC 的 OID 集请求之前[\_交换机\_DELETE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)，过量驱动程序必须执行以下操作：

-   在删除 VPort 之前，过量驱动程序必须清除或移动驱动程序以前在 VPort 上设置的所有接收筛选器。 接收筛选器是通过 oid\_接收\_筛选器的 OID 请求设置的， [\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)，并通过 OID [\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)的 oid 请求移动\_筛选器进行移动。\_

-   过量驱动程序将 NDIS\_NIC 的**VPortId**成员设置[ **\_交换机\_DELETE\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构设置为要删除的非默认 VPORT 的标识符。

    **请注意**  过量驱动程序不得将**VPortId**成员设置为**NDIS\_默认\_端口\_号**。 此 VPort 标识符保留用于连接到网络适配器上 PCI Express （PCIe）物理功能（PF）的默认 VPort。 默认 VPort 始终存在，但不会通过 OID [\_NIC\_开关\_DELETE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)中显式删除。

     

过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) [\_\_NIC 发出 OID，\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)请求到基础 PF 微型端口驱动程序。 当微型端口驱动程序接收 OID\_NIC\_交换机\_DELETE\_VPORT 请求时，驱动程序必须执行以下操作：

-   驱动程序必须释放为指定的 VPort 分配的硬件和软件资源。

-   驱动程序必须从 PF 或 PCIe 虚函数（VF）分离指定的 VPort。

    如果将 VPort 附加到 VF，则虚拟化堆栈会确保已暂停和暂停来宾操作系统中运行的 VF 微型端口驱动程序。 因此，所有 previouslyindicated 从 VPort 接收数据包都应该已经返回到 VF 微型端口驱动程序。

    如果 VPort 附加到 PF，则 PF 微型端口驱动程序必须停止与 VPort 关联的共享内存的任何附加 DMA。 PF 微型端口驱动程序必须确保将 VPort 中的所有 previouslyindicated 接收数据包返回到小型端口。 PF 小型端口驱动程序不得为 NDIS 指定在数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中指定 VPort 标识符的任何其他接收指示。 将 VPort 中的所有指定接收数据包返回到 PF 微型端口驱动程序后，必须通过调用[**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)来释放与 VPort 关联的共享内存。

以下几点适用于删除 VPorts：

-   过量协议驱动程序必须删除其在调用[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)之前创建的所有非默认 VPorts。

-   过量筛选器驱动程序必须删除其在其[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数内创建的所有非默认 VPorts。

-   在 NDIS 发出\_NIC 的 OID 的 set 请求之前[\_交换机\_delete\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)来删除网络适配器上的 NIC 交换机，这可保证从该交换机删除所有非默认 VPorts。

-   只有非默认的 VPorts 才能通过 oid [\_NIC\_交换机\_DELETE\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)显式删除。 当 PF 微型端口驱动程序删除默认 NIC 交换机时，会隐式删除默认 VPort。 有关详细信息，请参阅[删除 NIC 交换机](deleting-a-nic-switch.md)。

 

 





