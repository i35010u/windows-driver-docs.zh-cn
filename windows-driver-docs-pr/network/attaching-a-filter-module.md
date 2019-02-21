---
title: 将附加筛选器模块
description: 将附加筛选器模块
ms.assetid: 4441383e-cc22-4fe1-9c46-28d405736daa
keywords:
- 筛选器模块 WDK 连接网络、 附加
- 将附加筛选器模块
- 筛选器驱动程序 WDK 网络，将附加筛选器模块
- NDIS 筛选器驱动程序 WDK，附加筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f7ffa1d78fcbb925563ba8acd281d2e25f780f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542659"
---
# <a name="attaching-a-filter-module"></a>将附加筛选器模块





若要启动筛选器模块插入驱动程序堆栈的过程，NDIS 调用筛选器驱动程序[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数。 在中执行的起始*FilterAttach*函数，筛选器模块进入*附加*状态。 有关将筛选器模块附加到驱动程序堆栈的详细信息，请参阅[启动驱动程序堆栈](starting-a-driver-stack.md)。

筛选器驱动程序使用 NDIS 将在传递的句柄*NdisFilterHandle*的参数[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)所有将来**NdisXxx**请参阅此筛选器模块的函数调用。 此类函数包括状态指示，将请求发送、 接收的指示和 OID 请求。

在筛选器模块时*附加*状态时，该驱动程序：

-   创建筛选器模块的上下文区域并分配缓冲池和其他筛选器特定于模块资源。 有关缓冲池的详细信息，请参阅[筛选器驱动程序缓冲区管理](filter-driver-buffer-management.md)。

-   调用[ **NdisFSetAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff562619)函数通过使用*NdisFilterHandle* NDIS 传递到值[ *FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905). *FilterModuleContext*的参数**NdisFSetAttributes**指定此筛选器模块的筛选器驱动程序的上下文区域。 NDIS 将此上下文区域传递给筛选器驱动程序*FilterXxx*函数。

-   （可选） 从注册表中读取此筛选器模块的配置参数。 有关详细信息，请参阅[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

-   如果已成功完成上述操作，筛选器模块位于*已暂停*状态。

-   如果上述操作失败，筛选器驱动程序必须释放它分配中的资源[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数，并返回到筛选器模块*Detached*状态。

-   返回 NDIS\_状态\_成功或相应的故障代码。 如果该驱动程序返回了失败代码，NDIS 终止驱动程序堆栈。

**请注意**  注册表可能包含一个标志，指定筛选器模块，是可选的。 如果未附加的可选筛选器模块，NDIS 不会终止驱动程序堆栈的其余部分。

 

筛选器驱动程序不能进行发送请求、 指示接收到的数据、 发出 OID 请求或进行中的状态指示*附加*状态。 发送和接收操作中支持*运行*并*暂停*状态。 中支持 OID 请求以及状态表明*已暂停*，*正在重新启动*，*运行*，以及*暂停*状态。

NDIS 调用[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)函数可分离 NDIS 附加了一个筛选器模块[ *FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)。 有关详细信息，请参阅[分离筛选器模块](detaching-a-filter-module.md)。

 

 





