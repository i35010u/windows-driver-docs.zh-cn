---
title: 清除 VMQ 筛选器
description: 清除 VMQ 筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e3061b815a01c517da834c0050592163d22887
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826973"
---
# <a name="clearing-a-vmq-filter"></a>清除 VMQ 筛选器





若要在接收队列中释放筛选器，过量驱动程序 [会发出 oid \_ 接收筛选器 \_ \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md) 设置 oid 请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ CLEAR \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构的指针。

协议驱动程序从较早的 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器方法 OID 请求获取了筛选器标识符。 有关设置筛选器的详细信息，请参阅 [设置 VMQ 筛选器](setting-a-vmq-filter.md)。

协议驱动程序必须在队列释放队列之前清除它在队列上设置的所有筛选器。 协议驱动程序还必须清除它在默认队列上设置的所有筛选器，然后再将其绑定到网络适配器。

如果某个小型小型驱动程序已完成 OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器 oid 请求以清除该队列上的最后一个筛选器，或者它已完成 [oid \_ 接收 \_ 筛选器 \_ 免费 \_ 队列](./oid-receive-filter-free-queue.md) OID 请求来释放队列，则该驱动程序不能在非默认队列中指示数据包。

 

