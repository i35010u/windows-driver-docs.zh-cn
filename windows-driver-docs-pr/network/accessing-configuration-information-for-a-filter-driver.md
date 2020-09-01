---
title: 访问筛选器驱动程序的配置信息
description: 访问筛选器驱动程序的配置信息
ms.assetid: 7d6bd7d4-3c06-4fc3-874b-fb8369ac227e
keywords:
- 筛选器驱动程序 WDK 网络，配置信息
- NDIS 筛选器驱动程序 WDK，配置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 286f7b26edde0064083f405b93d5e3dbc4df3341
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214032"
---
# <a name="accessing-configuration-information-for-a-filter-driver"></a>访问筛选器驱动程序的配置信息





NDIS 支持一组函数，这些函数提供对筛选器驱动程序注册表参数的访问。 筛选器驱动程序可以在附加或重启操作期间或在处理即插即用 (PnP) 通知时访问这些参数。 有关 PnP 通知的详细信息，请参阅 [筛选器模块 PnP 事件通知](filter-module-pnp-event-notifications.md)。 有关附加筛选器模块的详细信息，请参阅 [附加筛选器模块](attaching-a-filter-module.md)。 有关重新启动操作的详细信息，请参阅 [启动筛选器模块](starting-a-filter-module.md)。

筛选器驱动程序调用 [**NdisOpenConfigurationEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex) 函数来访问注册表设置。 如果筛选器驱动程序通过调用[**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数获取了[**NDIS \_ 配置 \_ 对象**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)结构的**NdisHandle**成员中的句柄，则**NdisOpenConfigurationEx**函数将提供存储筛选器驱动程序的配置参数的注册表位置的句柄。 在调用 [**NdisFDeregisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver) 函数之前，筛选器驱动程序可以使用配置句柄。

如果筛选器驱动程序在**NdisHandle**中从[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的*NdisFilterHandle*参数获取了句柄，则[**NdisOpenConfigurationEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)将提供存储筛选器模块的配置参数的注册表位置的句柄。 筛选器驱动程序可以使用配置句柄，直到 NDIS 分离筛选器模块并且 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数返回。 如果监视筛选器驱动程序 \_ \_ \_ \_ \_ 在[**ndis \_ 配置 \_ 对象**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)结构的**Flags**成员中指定了 ndis CONFIG 标志筛选器实例配置标志，则当存在通过相同的小型小型适配器配置的多个筛选器模块时，驱动程序可以访问特定筛选器模块的筛选器模块配置。 修改筛选器驱动程序不能使用此标志。

完成访问配置信息的驱动程序后，驱动程序必须调用 [**NdisCloseConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration) 函数以释放配置句柄和相关资源。

 

