---
title: 查询数据包的可扩展交换机源端口数据
description: 查询数据包的可扩展交换机源端口数据
ms.assetid: 082AEF58-3FCF-4ABE-90E1-1AC5DAF32B54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8749e6ac25f0f6ca48da5bbd9711dbd5ac79d6e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385436"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>查询数据包的可扩展交换机源端口数据


指定的 HYPER-V 可扩展交换机源端口**SourcePortId**中的成员[ **NDIS\_切换\_转发\_详细\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。 此结构包含在带外 (OOB) 转发的数据包的上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 在此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展访问[ **NDIS\_切换\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构的[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。 下面的示例演示如何驱动程序可以从该数据包中获取源端口标识符**NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**结构。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

 





