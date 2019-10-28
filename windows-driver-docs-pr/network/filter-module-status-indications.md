---
title: 筛选器模块状态指示
description: 筛选器模块状态指示
ms.assetid: b39c6cda-dac7-4538-8ea6-513a52601b1f
keywords:
- 筛选器模块 WDK 网络，状态指示
- 筛选器驱动程序 WDK 网络，状态指示
- NDIS 筛选器驱动程序 WDK，状态指示
- 状态指示 WDK 网络，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26fa7ad0a603c09d75e7e9b7bdf4d60f85ef5054
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838110"
---
# <a name="filter-module-status-indications"></a>筛选器模块状态指示





筛选器驱动程序可以提供一个[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数，该函数在基础驱动程序报告状态时 NDIS 调用。 筛选器驱动程序还可以启动状态指示。

下图说明了筛选后的状态指示。

![说明筛选的状态指示的关系图](images/statusfilter.png)

在基础驱动程序调用状态指示函数（[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)或[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)）之后，NDIS 调用筛选器驱动程序的[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数。 有关如何从微型端口驱动程序指示状态的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

筛选器驱动程序在其[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数中调用**NdisFIndicateStatus** ，以便将筛选状态指示传递到过量驱动程序。 筛选器驱动程序可以筛选出状态指示（不调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)），也可以在调用**NdisFIndicateStatus**之前修改指示的状态。

若要产生状态指示，则筛选驱动程序调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) ，而无需事先调用[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)。

在这种情况下，筛选器驱动程序应将**SourceHandle**成员设置为 NDIS 传递到[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的*NdisFilterHandle*参数的句柄。 如果状态指示与 OID 请求关联，则筛选器驱动程序可以设置**DestinationHandle**和**RequestId**成员，使 NDIS 能够向特定协议绑定提供状态指示。

筛选器驱动程序调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)后，NDIS 将调用下一个过量驱动程序的状态函数（[**ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)或*FilterStatus*）。

 

 





