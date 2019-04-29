---
title: 访问筛选器驱动程序的配置信息
description: 访问筛选器驱动程序的配置信息
ms.assetid: 7d6bd7d4-3c06-4fc3-874b-fb8369ac227e
keywords:
- 筛选器驱动程序 WDK 网络配置信息
- NDIS 筛选器驱动程序 WDK，配置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685f4d987c61a325c54ff1921c0be43de432cc49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367891"
---
# <a name="accessing-configuration-information-for-a-filter-driver"></a>访问筛选器驱动程序的配置信息





NDIS 支持一组提供访问权限筛选器驱动程序注册表参数的函数。 筛选器驱动程序可以在连接期间访问这些参数，或重新启动操作或当它们正在处理插 (PnP) 通知。 有关即插即用通知的详细信息，请参阅[筛选器模块即插即用事件通知](filter-module-pnp-event-notifications.md)。 有关附加筛选器模块的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。 有关重新启动操作的详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

筛选驱动程序调用[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)函数来访问注册表设置。 如果筛选器驱动程序获取的手柄**NdisHandle**的成员[ **NDIS\_配置\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff564866)通过调用的结构[ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)函数， **NdisOpenConfigurationEx**函数提供的句柄注册表位置的筛选器存储驱动程序的配置参数。 筛选器驱动程序可以使用配置句柄，直到它们调用[ **NdisFDeregisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff561800)函数。

如果筛选器驱动程序获取的手柄**NdisHandle**从*NdisFilterHandle*参数[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数，[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)提供筛选器模块的配置参数的存储位置的注册表位置的句柄。 筛选器驱动程序可以使用配置句柄，直到 NDIS 分离筛选器模块和[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)函数返回。 如果监视的筛选器驱动程序指定 NDIS\_CONFIG\_标志\_筛选器\_实例\_中的配置标记**标志**隶属[**NDIS\_配置\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff564866)结构，当多个筛选器模块时，该驱动程序可以访问特定筛选器模块的筛选器模块配置，通过相同的微型端口适配器配置。 修改筛选器驱动程序必须使用此标志。

驱动程序完成后访问的配置信息，该驱动程序必须调用[ **NdisCloseConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff561642)函数，以释放配置句柄和相关的资源。

 

 





