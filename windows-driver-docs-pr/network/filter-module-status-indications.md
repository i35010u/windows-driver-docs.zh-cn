---
title: 筛选器模块状态指示
description: 筛选器模块状态指示
keywords:
- 筛选器模块 WDK 网络，状态指示
- 筛选器驱动程序 WDK 网络，状态指示
- NDIS 筛选器驱动程序 WDK，状态指示
- 状态指示 WDK 网络，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18f16dfe974bf9de5210ec2ada2dd4fc8dd40c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805243"
---
# <a name="filter-module-status-indications"></a>筛选器模块状态指示





筛选器驱动程序可以提供一个 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status) 函数，该函数在基础驱动程序报告状态时 NDIS 调用。 筛选器驱动程序还可以启动状态指示。

下图说明了筛选后的状态指示。

![说明筛选的状态指示的关系图](images/statusfilter.png)

在基础驱动程序 ([**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)或 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)) 调用状态指示函数后，NDIS 调用筛选器驱动程序的 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数。 有关如何从微型端口驱动程序指示状态的详细信息，请参阅 [适配器状态指示](miniport-adapter-status-indications.md)。

筛选器驱动程序在其 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数中调用 **NdisFIndicateStatus** ，以便将筛选状态指示传递到过量驱动程序。 筛选器驱动程序可以通过不调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 来筛选出状态指示 () 或在调用 **NdisFIndicateStatus** 之前修改指示的状态。

若要产生状态指示，则筛选驱动程序调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) ，而无需事先调用 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)。

在这种情况下，筛选器驱动程序应将 **SourceHandle** 成员设置为 NDIS 传递到 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的 *NdisFilterHandle* 参数的句柄。 如果状态指示与 OID 请求关联，则筛选器驱动程序可以设置 **DestinationHandle** 和 **RequestId** 成员，使 NDIS 能够向特定协议绑定提供状态指示。

筛选器驱动程序调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)后，NDIS 会调用状态函数， ([**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) 或 *FilterStatus*) 下一个过量驱动程序。

 

