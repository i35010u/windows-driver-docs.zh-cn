---
title: 访问筛选器驱动程序的配置信息
description: 访问筛选器驱动程序的配置信息
ms.assetid: 7d6bd7d4-3c06-4fc3-874b-fb8369ac227e
keywords:
- 筛选器驱动程序 WDK 网络，配置信息
- NDIS 筛选器驱动程序 WDK，配置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d1106e45050ccd245964e5169151894b0104018
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835397"
---
# <a name="accessing-configuration-information-for-a-filter-driver"></a>访问筛选器驱动程序的配置信息





NDIS 支持一组函数，这些函数提供对筛选器驱动程序注册表参数的访问。 筛选器驱动程序可以在附加或重启操作期间或在处理即插即用（PnP）通知时访问这些参数。 有关 PnP 通知的详细信息，请参阅[筛选器模块 PnP 事件通知](filter-module-pnp-event-notifications.md)。 有关附加筛选器模块的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。 有关重新启动操作的详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

筛选器驱动程序调用[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)函数来访问注册表设置。 如果筛选器驱动程序在[**NDIS\_配置\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)结构的**NdisHandle**成员中获取了句柄，则调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数， **NdisOpenConfigurationEx**函数提供存储筛选器驱动程序的配置参数的注册表位置的句柄。 在调用[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)函数之前，筛选器驱动程序可以使用配置句柄。

如果筛选器驱动程序在**NdisHandle**中从[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的*NdisFilterHandle*参数获取了句柄，则[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)将为注册表位置提供一个句柄，其中筛选器模块的存储配置参数。 筛选器驱动程序可以使用配置句柄，直到 NDIS 分离筛选器模块并且[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数返回。 如果监视筛选器驱动程序在[**ndis\_配置\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)结构的**Flags**成员中指定 NDIS\_CONFIG\_标志\_FILTER\_实例\_配置标志，则当有多个在同一微型端口适配器上配置的筛选器模块时，驱动程序可以访问特定筛选器模块的筛选器模块配置。 修改筛选器驱动程序不能使用此标志。

完成访问配置信息的驱动程序后，驱动程序必须调用[**NdisCloseConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)函数以释放配置句柄和相关资源。

 

 





