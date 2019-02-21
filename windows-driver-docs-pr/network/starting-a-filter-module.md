---
title: 启动筛选器模块
description: 启动筛选器模块
ms.assetid: 493cb922-22bc-4845-b5a2-6f610559534d
keywords:
- 筛选器模块 WDK 网络启动
- 启动筛选器模块
- 筛选器驱动程序 WDK 网络启动筛选器模块
- NDIS 筛选器驱动程序 WDK，开始筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4adf0795f8999e9da68b214528382538c8ba5cdc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523876"
---
# <a name="starting-a-filter-module"></a>启动筛选器模块





若要启动暂停的筛选器模块，NDIS 调用筛选器驱动程序[ *FilterSetModuleOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549970)函数，如果有，然后通过调用[ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)函数。 筛选器模块进入*正在重新启动*中执行的开始处的状态*FilterRestart*函数。

如果该驱动程序提供的入口点[ *FilterSetModuleOptions*](https://msdn.microsoft.com/library/windows/hardware/ff549970)，驱动程序可以更改筛选器模块的部分特性。 有关详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

当它调用筛选器驱动程序[ *FilterRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff549962)函数，NDIS 将传递一个指向[ **NDIS\_重启\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)结构中的筛选器驱动程序**RestartAttributes**的成员[ **NDIS\_筛选器\_重新启动\_参数** ](https://msdn.microsoft.com/library/windows/hardware/ff565572)结构。 筛选器驱动程序可以修改由基础驱动程序指定的重启属性。 有关如何修改重启属性的详细信息，请参阅*FilterRestart*。

**请注意**  NDIS 调用[ *FilterSetModuleOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549970)对于所有筛选器之前 NDIS 调用堆栈中的模块[ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)堆栈中的任何筛选器模块的函数。

 

NDIS 插操作，重新启动驱动程序堆栈的一部分启动筛选器模块。 重新启动驱动程序堆栈的概述，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

在筛选器模块代表*正在重新启动*状态时，筛选器驱动程序：

-   完成重新启动正常发送和接收操作所需的任何操作。

    有关详细信息大约发送和接收操作，请参阅[筛选器模块发送和接收操作](filter-module-send-and-receive-operations.md)。

-   可以读取或写入筛选器模块的可配置参数。

-   可以接收网络数据的指示。 该驱动程序可以复制和此类数据进行排队，并指定到更高版本，过量驱动程序或它可以丢弃数据。

-   应启动任何新的接收的指示。

-   应拒绝对所做的所有新发送请求其[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)立即通过调用函数[ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)函数。 它应在每个设置的完整状态[NET\_缓冲区\_列表](net-buffer-list-structure.md)到 NDIS\_状态\_已暂停。

-   可以提供与状态指示[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)函数。

    有关状态指示的详细信息，请参阅[筛选器模块状态指示](filter-module-status-indications.md)。

-   应处理中的 OID 请求[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)函数。

    有关 OID 的请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

-   应启动任何新的发送请求。

-   应返回新接收到 NDIS 指示立即通过调用[ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)函数。 如果有必要，驱动程序可以将复制此类之前将它们返回收到的指示。

-   可以对基础驱动程序设置进行 OID 请求或查询更新的配置信息。

-   应处理状态指示在其[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)函数。

-   应指示 NDIS\_状态\_成功或失败状态。 如果筛选器模块不会重启，NDIS 将其分离，然后如果它是必需的筛选器，NDIS 终止整个驱动程序堆栈。

筛选器驱动程序已成功重启发送和接收操作后，它必须完成的重新启动操作。 筛选器驱动程序可以完成的重新启动操作以同步方式还是以异步方式返回 NDIS\_状态\_成功或 NDIS\_状态\_分别从 PENDING [ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)。

如果该驱动程序返回 NDIS\_状态\_挂起，它必须调用[ **NdisFRestartComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562610)函数后重启操作。 在这种情况下，他驱动程序将传递到重新启动操作的最终状态**NdisFRestartComplete**。

重新启动操作已完成后，筛选器模块处于*运行*状态。 驱动程序继续正常发送和接收处理。

NDIS 并不会启动其他插操作，例如，附加、 分离，或暂停请求，在筛选器驱动程序时*正在重新启动*状态。 NDIS 筛选器驱动程序中后可以启动暂停请求*运行*状态。 有关暂停的筛选器模块的详细信息，请参阅[暂停筛选器模块](pausing-a-filter-module.md)。

 

 





