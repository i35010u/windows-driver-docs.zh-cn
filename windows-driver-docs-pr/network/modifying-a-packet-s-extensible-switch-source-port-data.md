---
title: 修改数据包的可扩展交换机源端口数据
description: 修改数据包的可扩展交换机源端口数据
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8296ae6c43256124504d2e4762ca6c6917c1825f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844225"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>修改数据包的可扩展交换机源端口数据


Hyper-v 可扩展交换机源端口由 NDIS\_交换机中的**SourcePortId**成员指定[ **\_转发\_详细信息\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。 此结构包含在数据包的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）转发上下文\_列表结构。 有关此上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展必须遵循以下准则来修改数据包的源端口标识符：

-   可扩展交换机扩展必须调用[*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)来修改数据包的源端口。 扩展不能直接修改 NDIS\_交换机的**SourcePortId**成员[ **\_转发\_详细信息\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。

-   如果扩展正在创建或克隆数据包，则它必须在调用[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)后调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)函数。 此函数为用于转发数据包信息的 OOB 数据分配可扩展的交换机上下文区域。

    当扩展调用[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)时， **SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**。 这会指定数据包源自扩展，而不是到达可扩展的交换机端口。

    具有 NDIS\_交换机的源端口的数据包 **\_默认\_端口\_ID**由可扩展交换机扩展数据路径视为特权和可信。 此类流量不应对应用于来自其他源端口的数据包的策略进行。 例如，具有 NDIS\_交换机的源端口标识符的数据包 **\_默认\_端口\_ID**会绕过可扩展交换机的基础微型端口边缘应用的内置可扩展交换机策略。 这些策略包括访问控制列表（Acl）和服务质量（QoS）。

    当扩展是源自数据包流量时，应慎用\_交换机的源端口 **\_默认\_端口\_ID** 。 在大多数情况下，扩展应将源端口标识符修改为可扩展交换机上的活动端口。 这允许将该端口的策略应用到该数据包。

    但是，在某些情况下，扩展必须使用 NDIS\_交换机的源端口 **\_默认\_端口\_ID**作为其源自的数据包。 例如，如果扩展插件产生了一个必须发送到其在物理或虚拟网络上的目标的控制数据包，则它应使用 **\_交换机\_默认\_端口标识符的\_ID** 。 这可确保包不会被可扩展交换机驱动程序堆栈中的基础扩展筛选和拒绝。

 

 





