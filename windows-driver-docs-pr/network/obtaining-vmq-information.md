---
title: 获取 VMQ 信息
description: 获取 VMQ 信息
ms.assetid: e851b656-ef59-42e7-b734-17ce9830096a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f418042f64095deda660170cc3e6a4b1ce9a79f7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217545"
---
# <a name="obtaining-vmq-information"></a>获取 VMQ 信息





VMQ 接口包含 OID 请求和 WMI Guid，它们允许过量的驱动程序和应用程序获取有关底层 VMQ 配置的信息。

[OID \_接收 \_ 筛选器 \_ 枚举 \_ 队列](./oid-receive-filter-enum-queues.md) 枚举在网络适配器上分配的队列。 有关枚举队列的详细信息，请参阅 [枚举已分配队列](enumerating-the-allocated-queues.md)。

作为方法 OID 请求，过量驱动程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](./oid-receive-filter-queue-parameters.md) OID 来获取特定队列的参数设置。 有关获取队列参数设置的详细信息，请参阅 [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md)。

[OID \_接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 枚举分配给特定队列的筛选器。 有关枚举在队列中设置的筛选器的详细信息，请参阅 [枚举 VMQ 上的筛选器](enumerating-filters-on-a-vmq.md)。

作为方法 OID 请求，过量驱动程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) oid 来获取筛选器的参数设置。 有关获取筛选器参数设置的详细信息，请参阅 [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md)。

过量驱动程序和应用程序可以发出以下 OID 查询请求，以获取 VMQ 功能。

[OID \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md)

[OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)

[OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数](./oid-receive-filter-global-parameters.md)

有关获取 VMQ 功能的详细信息，请参阅 [确定网络适配器的 Vmq 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

