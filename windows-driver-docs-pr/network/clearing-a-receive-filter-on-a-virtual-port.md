---
title: 清除虚拟端口上的接收筛选器
description: 清除虚拟端口上的接收筛选器
ms.assetid: 8431322B-2BF0-4F82-AAAE-0E0396BBC857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17670dd0d30b5dcb41847c8b90cf0c4878ac2c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835178"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>清除虚拟端口上的接收筛选器


为了清除 NIC 交换机上的虚拟端口（VPort）中的接收筛选器，过量驱动程序会发出一个对象标识符（OID）设置的[OID 请求，\_接收\_filter\_清楚地\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器的指针，\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

在过量驱动程序发出[OID\_接收\_filter\_清除\_filter](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)请求之前，它必须初始化[**NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构并将其设置为成员采用以下方式：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_ID。

-   必须将**FilterId**成员设置为筛选器标识符值，该驱动程序从较早的 OID 获取的筛选器标识符值[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)方法 OID 请求。 有关如何设置接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](setting-a-receive-filter-on-a-virtual-port.md)。

过量驱动程序必须清除它在 VPort 上设置的所有筛选器，然后才能释放 VPort。 过量驱动程序还必须清除它在默认 VPort 上设置的所有筛选器，然后将其绑定到网络适配器或从网络适配器分离。

 

 





