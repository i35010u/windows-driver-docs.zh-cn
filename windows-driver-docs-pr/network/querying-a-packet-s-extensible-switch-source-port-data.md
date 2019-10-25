---
title: 查询数据包的可扩展交换机源端口数据
description: 查询数据包的可扩展交换机源端口数据
ms.assetid: 082AEF58-3FCF-4ABE-90E1-1AC5DAF32B54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3938d6ada9671d0d06d0f4edf0653feb76648c44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844897"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>查询数据包的可扩展交换机源端口数据


Hyper-v 可扩展交换机源端口由 NDIS\_交换机中的**SourcePortId**成员指定[ **\_转发\_详细信息\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。 此结构包含在数据包的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）转发上下文\_列表结构。 有关此上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展使用 Net\_BUFFER\_LIST 访问[**NDIS\_交换机\_转发\_详细信息\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构[ **\_切换\_转发\_详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。 以下示例演示了驱动程序如何从数据包的 NDIS\_交换机获取源端口标识符 **\_转发\_详细信息\_NET\_BUFFER\_LIST\_INFO**结构。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

 





