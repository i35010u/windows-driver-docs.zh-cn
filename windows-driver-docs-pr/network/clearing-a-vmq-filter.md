---
title: 清除 VMQ 筛选器
description: 清除 VMQ 筛选器
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbd3b5d390aad74ea176d6e3acec983706506cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385536"
---
# <a name="clearing-a-vmq-filter"></a>清除 VMQ 筛选器





要释放接收队列中的筛选器，基础驱动程序将发出[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)集 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

从早期协议驱动程序获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)方法 OID 请求。 有关设置筛选器的详细信息，请参阅[VMQ 筛选器设置](setting-a-vmq-filter.md)。

协议驱动程序必须清除它在释放队列前在队列设置的所有筛选器。 协议驱动程序还必须清除它的默认队列，然后设置关闭其绑定到的网络适配器的所有筛选器。

微型端口驱动程序必须指示非默认队列上的数据包，如果它已完成 OID\_接收\_筛选器\_清除\_对清除队列上的最后一个筛选器或如果它已完成筛选器OID请求[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)OID 请求以释放队列。

 

 





