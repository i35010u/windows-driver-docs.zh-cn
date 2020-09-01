---
title: 修改数据包的可扩展交换机源端口数据
description: 修改数据包的可扩展交换机源端口数据
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690198db774bfbd402e40826e5d2afbf037a1319
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207457"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>修改数据包的可扩展交换机源端口数据


Hyper-v 可扩展交换机源端口由[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构中的**SourcePortId**成员指定。 此结构包含在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的带外 (OOB) 转发上下文中。 有关此上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展必须遵循以下准则来修改数据包的源端口标识符：

-   可扩展交换机扩展必须调用 [*SetNetBufferListSource*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source) 来修改数据包的源端口。 扩展不能直接修改[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构的**SourcePortId**成员。

-   如果扩展正在创建或克隆数据包，则它必须在调用[**NdisAllocateNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)后调用[*AllocateNetBufferListForwardingContext*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数。 此函数为用于转发数据包信息的 OOB 数据分配可扩展的交换机上下文区域。

    当扩展调用 [*AllocateNetBufferListForwardingContext*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)时， **SourcePortId** 成员将设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。 这会指定数据包源自扩展，而不是到达可扩展的交换机端口。

    具有 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 的源端口的数据包由可扩展交换机扩展数据路径视为特权和可信。 此类流量不应对应用于来自其他源端口的数据包的策略进行。 例如，具有 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 的源端口标识符的数据包会绕过可扩展交换机的基础微型端口边缘应用的内置可扩展交换机策略。 这些策略包括 (Acl) 和服务质量 (QoS) 的访问控制列表。

    当扩展是发起数据包流量时，应谨慎地使用 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 的源端口。 在大多数情况下，扩展应将源端口标识符修改为可扩展交换机上的活动端口。 这允许将该端口的策略应用到该数据包。

    但是，在某些情况下，扩展必须使用 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 的源端口来存储它所源自的数据包。 例如，如果扩展插件产生了一个必须发送到其在物理或虚拟网络上的目标的控制数据包，则应该为源端口标识符使用 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 。 这可确保包不会被可扩展交换机驱动程序堆栈中的基础扩展筛选和拒绝。

 

