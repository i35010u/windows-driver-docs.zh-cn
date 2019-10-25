---
title: 清除 VMQ 筛选器
description: 清除 VMQ 筛选器
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae482cc260d3e01aebc3b1c4addf900ef35f447
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838206"
---
# <a name="clearing-a-vmq-filter"></a>清除 VMQ 筛选器





为了释放接收队列中的筛选器，过量驱动程序会发出[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)设置 OID 请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器的指针，\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

协议驱动程序从较早的 OID 获取了筛选器标识符[\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)方法 OID 请求。 有关设置筛选器的详细信息，请参阅[设置 VMQ 筛选器](setting-a-vmq-filter.md)。

协议驱动程序必须在队列释放队列之前清除它在队列上设置的所有筛选器。 协议驱动程序还必须清除它在默认队列上设置的所有筛选器，然后再将其绑定到网络适配器。

如果某个微型端口驱动程序已完成 OID\_接收\_筛选器，则该驱动程序不能在非默认队列上指示数据包，\_清除\_筛选 OID 请求以清除队列中的最后一个筛选器，或者如果已完成[oid\_接收\_FILTER\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)OID 请求，以释放队列。

 

 





