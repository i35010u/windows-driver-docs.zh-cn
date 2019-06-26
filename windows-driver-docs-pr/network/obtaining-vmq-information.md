---
title: 获取 VMQ 信息
description: 获取 VMQ 信息
ms.assetid: e851b656-ef59-42e7-b734-17ce9830096a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ea9d407739e4d17a8105bc6eb653caeb579b90b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354499"
---
# <a name="obtaining-vmq-information"></a>获取 VMQ 信息





VMQ 接口包含 OID 请求和允许过量驱动程序和应用程序可以获取基础 VMQ 配置信息的 WMI Guid。

[OID\_接收\_筛选器\_ENUM\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)枚举上的网络适配器分配的队列。 有关枚举队列的详细信息，请参阅[枚举已分配队列](enumerating-the-allocated-queues.md)。

作为方法 OID 请求，过量驱动程序可以使用[OID\_接收\_筛选器\_队列\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)OID，若要获取特定队列的参数设置。 有关获取队列参数设置的详细信息，请参阅[Obtaining 和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)。

[OID\_接收\_筛选器\_ENUM\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)枚举特定队列分配的筛选器。 有关枚举在队列设置的筛选器的详细信息，请参阅[VMQ 的枚举筛选器](enumerating-filters-on-a-vmq.md)。

作为方法 OID 请求，过量驱动程序可以使用[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)OID，若要获取筛选器的参数设置。 有关获取筛选器参数设置的详细信息，请参阅[Obtaining 和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)。

过量驱动程序和应用程序可以发出以下 OID 查询请求以获取 VMQ 功能。

[OID\_RECEIVE\_FILTER\_HARDWARE\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

[OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

[OID\_接收\_筛选器\_GLOBAL\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

有关获取 VMQ 功能的详细信息，请参阅[确定网络适配器的 VMQ 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

 





