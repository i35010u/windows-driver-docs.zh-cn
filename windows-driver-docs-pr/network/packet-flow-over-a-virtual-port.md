---
title: 基于虚拟端口的数据包流
description: 基于虚拟端口的数据包流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8f2838296d3027d3082f935ab1cf4e06020c495
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829197"
---
# <a name="packet-flow-over-a-virtual-port"></a>基于虚拟端口的数据包流


默认 NIC 交换机是网络适配器的一个组件，它支持 (SR-IOV) 接口的单个根 i/o 虚拟化。 开关始终将 (VPort) 的默认虚拟端口附加到 PCI Express (PCIe) 物理函数 (PF) 。 开关可以将一个或多个非默认 VPorts 附加到 PF。 有关详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

以下几点适用于在附加到 PF 的 VPort 上发送或接收的数据包：

-   使用 **默认 \_ VPort \_ ID** 的 VPort 标识符值指定在默认 VPort 上发送或接收的数据包。

    通过使用 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md)的 oid 方法请求创建 VPort 时返回的 VPort 标识符，指定通过非默认 VPorts 发送或接收的数据包。 当驱动程序处理此 OID 请求时，它将从与 OID 请求关联的 [**NDIS \_ NIC \_ 交换机 \_ VPort \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的 **VPortId** 成员获取 VPort 标识符。

    **注意**  删除 VPort 时，微型端口驱动程序可以接收包含无效 **VPortId** 值的 NBL。 如果发生这种情况，微型端口应忽略无效的 VPort ID，并改为使用 **默认 \_ VPort \_ id** 。 **VPortId** 在 NBL 的 OOB 数据的 **NetBufferListFilteringInfo** 部分中找到，并使用 [**NET \_ BUFFER \_ LIST \_ RECEIVE \_ FILTER \_ VPORT \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_vport_id)宏检索。

     

-   PF 微型端口驱动程序调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) ，以指示从 VPort 接收的数据包。 在 PF 微型端口驱动程序调用 **NdisMIndicateReceiveNetBufferLists** 之前，必须在包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中的带外 (OOB) 数据中设置 VPort 标识符。 该驱动程序通过使用 [**NET \_ BUFFER \_ LIST \_ RECEIVE \_ FILTER \_ VPORT \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_vport_id) 宏来实现此功能。

-   虚拟化堆栈调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) 将数据包传输到 VPort。 在虚拟化堆栈调用 **NdisSendNetBufferLists** 之前，它会在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的 OOB 数据中设置 VPort 标识符。

    微型端口驱动程序通过使用 [**NET \_ BUFFER \_ LIST \_ RECEIVE \_ FILTER \_ VPort \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_vport_id) 宏获取 VPort 标识符。

    微型端口驱动程序必须在指定 VPort 的硬件传输队列中对传输数据包进行排队。

**注意**  PCIe 虚拟功能 (VF) 的微型端口驱动程序未在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的 OOB 数据中设置或查询 VPort 标识符。 当 VF 微型端口驱动程序发送数据包时，它将对附加到 VF 的单个非默认 VPort 的硬件传输队列中的数据包进行排队。

 

 

