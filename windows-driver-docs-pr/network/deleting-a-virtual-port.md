---
title: 删除虚拟端口
description: 删除虚拟端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7034ce4ce3555c4559d3d3d009228dce641575
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248364"
---
# <a name="deleting-a-virtual-port"></a>删除虚拟端口


过量驱动程序会 (OID 发出对象标识符) 设置 [oid \_ nic \_ 交换机 \_ delete \_ VPORT](./oid-nic-switch-delete-vport.md) 以删除网络适配器的 NIC 交换机上的非默认虚拟端口 (VPORT) 。 过量驱动程序只能通过发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md)的 oid 方法请求，删除先前创建的 VPort。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ SWITCH \_ DELETE \_ VPORT \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构的指针。

过量驱动程序（例如虚拟化堆栈）可以删除先前创建的非默认 VPort。 过量驱动程序通过发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md)的 Oid 方法请求来创建一个 VPort。

在发出 oid [ \_ NIC \_ SWITCH \_ DELETE \_ VPORT](./oid-nic-switch-delete-vport.md)的 oid 集请求之前，过量驱动程序必须执行以下操作：

-   在删除 VPort 之前，过量驱动程序必须清除或移动驱动程序以前在 VPort 上设置的所有接收筛选器。 接收筛选器通过 oid [ \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) 的 oid 请求进行设置，并通过 oid [ \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md)的 oid 请求进行移动。

-   过量驱动程序将 [**NDIS \_ NIC \_ 交换机 \_ DELETE \_ VPORT \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构的 **VPortId** 成员设置为要删除的非默认 VPORT 的标识符。

    **注意**  过量驱动程序不得将 **VPortId** 成员设置为 **NDIS \_ 默认 \_ 端口 \_ 号**。 此 VPort 标识符是为附加到 PCI Express (PCIe) 物理功能 (PF) 网络适配器上的默认 VPort 预留的。 默认 VPort 始终存在，但不会通过 OID [ \_ NIC \_ 开关 \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)的 oid 设置请求显式删除。

     

过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将 [OID \_ NIC \_ SWITCH \_ DELETE \_ VPORT](./oid-nic-switch-delete-vport.md) 请求发送到基础 PF 微型端口驱动程序。 当微型端口驱动程序收到 OID \_ NIC \_ 交换机 \_ DELETE \_ VPORT 请求时，驱动程序必须执行以下操作：

-   驱动程序必须释放为指定的 VPort 分配的硬件和软件资源。

-   驱动程序必须将指定的 VPort 从 PF 或 PCIe 虚函数分离 (VF) 。

    如果将 VPort 附加到 VF，则虚拟化堆栈会确保已暂停和暂停来宾操作系统中运行的 VF 微型端口驱动程序。 因此，所有 previouslyindicated 从 VPort 接收数据包都应该已经返回到 VF 微型端口驱动程序。

    如果 VPort 附加到 PF，则 PF 微型端口驱动程序必须停止与 VPort 关联的共享内存的任何附加 DMA。 PF 微型端口驱动程序必须确保将 VPort 中的所有 previouslyindicated 接收数据包返回到小型端口。 PF 小型端口驱动程序不得对在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构中指定 VPort 标识符的 NDIS 进行任何额外的接收指示。 将 VPort 中的所有指定接收数据包返回到 PF 微型端口驱动程序后，必须通过调用 [**NdisFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)来释放与 VPort 关联的共享内存。

以下几点适用于删除 VPorts：

-   过量协议驱动程序必须删除其在调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)之前创建的所有非默认 VPorts。

-   过量筛选器驱动程序必须删除其在其 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数内创建的所有非默认 VPorts。

-   在 NDIS 发出 [OID \_ nic \_ 交换机 \_ \_ ](./oid-nic-switch-delete-switch.md) 的 set 请求以删除网络适配器上的 nic 交换机之前，它可确保从该交换机中删除所有非默认 VPorts。

-   只有非默认 VPorts 可以通过 oid [ \_ NIC \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)的 oid 请求显式删除。 当 PF 微型端口驱动程序删除默认 NIC 交换机时，会隐式删除默认 VPort。 有关详细信息，请参阅 [删除 NIC 交换机](deleting-a-nic-switch.md)。

 

