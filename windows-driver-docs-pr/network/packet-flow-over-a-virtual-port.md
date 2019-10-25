---
title: 基于虚拟端口的数据包流
description: 基于虚拟端口的数据包流
ms.assetid: 1E4B1987-3288-4082-B8A8-0F275C61597F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe218833e36293906e2876a0cfec31c47a2c3e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843718"
---
# <a name="packet-flow-over-a-virtual-port"></a>基于虚拟端口的数据包流


默认 NIC 交换机是支持单根 i/o 虚拟化（SR-IOV）接口的网络适配器组件。 开关始终将默认的虚拟端口（VPort）附加到 PCI Express （PCIe）物理功能（PF）。 开关可以将一个或多个非默认 VPorts 附加到 PF。 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

以下几点适用于在附加到 PF 的 VPort 上发送或接收的数据包：

-   使用**默认\_VPort\_ID**的 VPort 标识符值指定在默认 VPort 上发送或接收的数据包。

    通过非默认 VPorts 发送或接收的数据包是使用 VPort 标识符指定的，该标识符是通过 oid [\_NIC\_交换机\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)创建的。 当驱动程序处理此 OID 请求时，它将从[**NDIS\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)的**VPortId**成员获取 VPORT 标识符，\_VPort 与 OID 请求关联的\_参数结构。

    **请注意**  在删除 VPort 时，微型端口驱动程序可以接收包含无效**VPORTID**值的 NBL。 如果发生这种情况，微型端口应忽略无效的 VPort ID，并改为使用**默认\_VPort\_id** 。 **VPortId**可在 NBL 的 OOB 数据的**NetBufferListFilteringInfo**部分找到，并使用[**NET\_BUFFER\_列表进行检索\_\_FILTER\_VPORT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)宏。

     

-   PF 微型端口驱动程序调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) ，以指示从 VPort 接收的数据包。 在 PF 微型端口驱动程序调用**NdisMIndicateReceiveNetBufferLists**之前，必须在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）数据中设置 VPort 标识符，\_包的列表结构。 驱动程序通过使用[**NET\_BUFFER\_列表\_接收\_FILTER\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)宏来实现此功能。

-   虚拟化堆栈调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)将数据包传输到 VPort。 在虚拟化堆栈调用**NdisSendNetBufferLists**之前，它会在[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中为数据包设置 VPort 标识符。

    微型端口驱动程序使用[**NET\_缓冲区\_列表获取 VPort 标识符，\_接收\_FILTER\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)宏。

    微型端口驱动程序必须在指定 VPort 的硬件传输队列中对传输数据包进行排队。

**请注意**  PCIe 虚拟功能（VF）的微型端口驱动程序未在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的 OOB 数据中设置或查询包的 VPort 标识符\_列表结构。 当 VF 微型端口驱动程序发送数据包时，它将对附加到 VF 的单个非默认 VPort 的硬件传输队列中的数据包进行排队。

 

 

 





