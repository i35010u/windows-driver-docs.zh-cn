---
title: 筛选器模块状态指示
description: 筛选器模块状态指示
ms.assetid: b39c6cda-dac7-4538-8ea6-513a52601b1f
keywords:
- 筛选器模块 WDK 网络状态指示
- 筛选器驱动程序 WDK 网络状态指示
- NDIS 筛选器驱动程序 WDK，状态指示
- 状态指示 WDK 网络筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de338b19ad86a3616ef289b66ee449e4af48c831
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363393"
---
# <a name="filter-module-status-indications"></a>筛选器模块状态指示





筛选器驱动程序可以提供[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status) NDIS 调用时基础驱动程序将状态报告函数。 筛选器驱动程序还可以启动状态的指示。

下图说明了一个经过筛选的状态说明。

![说明的筛选的状态指示的关系图](images/statusfilter.png)

NDIS 筛选器驱动程序将调用[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数后基础驱动程序调用的状态指示函数, ([**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)或[ **NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus))。 有关如何以指示从微型端口驱动程序状态的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

筛选器驱动程序调用**NdisFIndicateStatus**在其[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数，传递到过量驱动程序的筛选的状态指示。 筛选器驱动程序可以筛选出状态指示 (通过不调用[ **NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)) 或修改所指示的状态，然后它会调用**NdisFIndicateStatus**。

若要生成状态指示，筛选驱动程序调用[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)而无需调用之前[ *FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)。

在这种情况下，应设置筛选器驱动程序**SourceHandle**成员添加到 NDIS 传递给的句柄*NdisFilterHandle*参数[ *FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数。 如果使用 OID 请求相关联的状态指示，则可以设置筛选器驱动程序**DestinationHandle**并**RequestId**成员，因此该 NDIS 可以提供到特定协议的状态指示绑定。

筛选器驱动程序调用后[ **NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)，NDIS 调用状态函数 ([**ProtocolStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)或*FilterStatus*) 的下一步基础驱动程序。

 

 





