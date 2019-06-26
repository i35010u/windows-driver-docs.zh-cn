---
title: 删除虚拟端口
description: 删除虚拟端口
ms.assetid: CBE7AC59-D878-44BA-8FE6-168EC17A2D67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0c565b9898a33be0e8c3c58941d59a2dbbc58e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384562"
---
# <a name="deleting-a-virtual-port"></a>删除虚拟端口


基础驱动程序发出的一个对象标识符 (OID) 组请求[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)若要删除的网络适配器上的非默认虚拟端口 (VPort)NIC 开关。 基础驱动程序时，才能删除它之前已创建通过发出的 OID 方法请求 VPort [OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_删除\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构。

基础驱动程序，如虚拟化堆栈中，可以删除非默认 VPort 以前创建了它。 基础驱动程序通过发出的 OID 方法请求创建 VPort [OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

它会发出 OID 集请求的前[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)，基础驱动程序必须执行以下操作：

-   基础驱动程序必须删除或移动的所有接收该驱动程序之前设置 VPort 删除 VPort 之前的筛选器。 接收的 OID 请求通过设置筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)并且通过 OID 请求的移动[OID\_接收\_筛选器\_移动\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)。

-   过量的驱动程序集**VPortId**的成员[ **NDIS\_NIC\_开关\_删除\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构为非默认 VPort 要删除的标识符。

    **请注意**  过量的驱动程序必须未设置**VPortId**成员添加到**NDIS\_默认\_端口\_数**。 默认情况下附加到 PCI Express (PCIe) 物理函数 (PF) 网络适配器上的 VPort 保留此 VPort 标识符。 VPort 始终存在，以及删除不明确，但 OID 设置的请求的默认值[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)。

     

过量的驱动程序调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)颁发[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)对基础 PF 微型端口驱动程序的请求。 当微型端口驱动程序收到 OID\_NIC\_交换机\_删除\_VPORT 请求，该驱动程序必须执行以下操作：

-   该驱动程序必须释放已分配给指定 VPort 的硬件和软件资源。

-   该驱动程序必须分离指定的 VPort 从 PF 或 PCIe 虚拟函数 (VF)。

    如果 VPort 附加到 VF，虚拟化堆栈可确保，在来宾操作系统中运行的 VF 微型端口驱动程序具有先前已暂停并暂停。 因此，所有 previouslyindicated VPort 从都接收数据包时应已返回到 VF 微型端口驱动程序。

    如果 VPort 附加到 PF，PF 微型端口驱动程序必须停止任何其他 DMA VPort 与相关联的共享内存。 PF 微型端口驱动程序必须确保所有 previouslyindicated VPort 从都接收数据包返回到微型端口。 PF 微型端口驱动程序必须不进行任何其他接收到的数据包中指定 VPort 的标识符的 NDIS 迹象[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 所指示的所有接收数据包从 VPort 后将返回到 PF 微型端口驱动程序，则它必须释放通过调用与 VPort 相关联的共享的内存[ **NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreesharedmemory)。

以下几点适用于 VPorts 删除：

-   基础协议驱动程序必须删除所有非默认之前创建的 VPorts 调用[ **NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)。

-   基础筛选器驱动程序必须删除所有非默认 VPorts 它在创建其[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)函数。

-   NDIS 发出 set 请求的前[OID\_NIC\_切换\_删除\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)若要删除的网络适配器上的 NIC 交换机，它保证会删除所有非默认 VPorts从该交换机。

-   非默认，可以通过 OID 请求的显式删除 VPorts [OID\_NIC\_交换机\_删除\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 PF 微型端口驱动程序删除默认 NIC 交换机时，默认 VPort 是隐式删除。 有关详细信息，请参阅[删除 NIC 交换机](deleting-a-nic-switch.md)。

 

 





