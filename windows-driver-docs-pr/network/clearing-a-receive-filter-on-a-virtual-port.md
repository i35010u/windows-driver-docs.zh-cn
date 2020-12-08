---
title: 清除虚拟端口上的接收筛选器
description: 清除虚拟端口上的接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10d406d634d8599bc277e1d34f5c22ef718b9a2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787275"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>清除虚拟端口上的接收筛选器


若要清除 NIC 交换机上的虚拟端口 (VPort) 中的接收筛选器，过量驱动程序会发出对象标识符 (OID) 设置 [oid \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md)的请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ CLEAR \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构的指针。

在过量驱动程序发出 [OID \_ 接收筛选 \_ 器 \_ clear \_ filter](./oid-receive-filter-clear-filter.md) 请求之前，它必须初始化 [**NDIS \_ 接收 \_ 筛选器 \_ clear \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters) 结构并按以下方式设置成员：

-   **QueueId** 成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   必须将 **FilterId** 成员设置为该驱动程序从较早的 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器方法 OID 请求获取的筛选器标识符值。 有关如何设置接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](setting-a-receive-filter-on-a-virtual-port.md)。

过量驱动程序必须清除它在 VPort 上设置的所有筛选器，然后才能释放 VPort。 过量驱动程序还必须清除它在默认 VPort 上设置的所有筛选器，然后将其绑定到网络适配器或从网络适配器分离。

 

