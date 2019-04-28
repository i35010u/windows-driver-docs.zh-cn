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
ms.openlocfilehash: 690e821a56e75e7a8ae736fa58032bf26c801c74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350026"
---
# <a name="filter-module-status-indications"></a>筛选器模块状态指示





筛选器驱动程序可以提供[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973) NDIS 调用时基础驱动程序将状态报告函数。 筛选器驱动程序还可以启动状态的指示。

下图说明了一个经过筛选的状态说明。

![说明的筛选的状态指示的关系图](images/statusfilter.png)

NDIS 筛选器驱动程序将调用[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)函数后基础驱动程序调用的状态指示函数, ([**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)或[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824))。 有关如何以指示从微型端口驱动程序状态的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

筛选器驱动程序调用**NdisFIndicateStatus**在其[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)函数，传递到过量驱动程序的筛选的状态指示。 筛选器驱动程序可以筛选出状态指示 (通过不调用[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824)) 或修改所指示的状态，然后它会调用**NdisFIndicateStatus**。

若要生成状态指示，筛选驱动程序调用[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)而无需调用之前[ *FilterStatus*](https://msdn.microsoft.com/library/windows/hardware/ff549973)。

在这种情况下，应设置筛选器驱动程序**SourceHandle**成员添加到 NDIS 传递给的句柄*NdisFilterHandle*参数[ *FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数。 如果使用 OID 请求相关联的状态指示，则可以设置筛选器驱动程序**DestinationHandle**并**RequestId**成员，因此该 NDIS 可以提供到特定协议的状态指示绑定。

筛选器驱动程序调用后[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824)，NDIS 调用状态函数 ([**ProtocolStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570270)或*FilterStatus*) 的下一步基础驱动程序。

 

 





