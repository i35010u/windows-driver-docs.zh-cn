---
title: 附加筛选器模块
description: 附加筛选器模块
ms.assetid: 4441383e-cc22-4fe1-9c46-28d405736daa
keywords:
- 筛选器模块 WDK 网络，附加
- 附加筛选器模块
- 筛选器驱动程序 WDK 网络，附加筛选器模块
- NDIS 筛选器驱动程序 WDK，附加筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cfd5c56d520ec515a4f82b9136e1c891545039
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215970"
---
# <a name="attaching-a-filter-module"></a>附加筛选器模块





为了启动将筛选器模块插入驱动程序堆栈的过程，NDIS 调用筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数。 在 *FilterAttach* 函数中的执行开始时，筛选器模块将进入 *附加* 状态。 有关将筛选器模块附加到驱动程序堆栈的详细信息，请参阅 [启动驱动程序堆栈](starting-a-driver-stack.md)。

筛选器驱动程序使用该句柄，该句柄通过引用此筛选器模块的所有未来**NdisXxx**函数调用中的[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)的*NdisFilterHandle*参数进行传递。 此类函数包括状态指示、发送请求、接收指示和 OID 请求。

当筛选器模块处于 *附加* 状态时，驱动程序将：

-   创建筛选器模块的上下文区域，并分配缓冲池和其他特定于筛选器模块的资源。 有关缓冲池的详细信息，请参阅 [筛选器驱动程序缓冲区管理](filter-driver-buffer-management.md)。

-   使用 NDIS 传递到[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)的*NdisFilterHandle*值调用[**NdisFSetAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsetattributes)函数。 **NdisFSetAttributes**的*FilterModuleContext*参数为此筛选器模块指定筛选器驱动程序的上下文区域。 NDIS 将此上下文区域传递到筛选器驱动程序的 *FilterXxx* 函数。

-   （可选）从注册表中读取此筛选器模块的配置参数。 有关详细信息，请参阅 [访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

-   如果前面的操作已成功完成，筛选器模块将处于 *暂停* 状态。

-   如果上述操作失败，筛选器驱动程序必须释放它在 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数中分配的任何资源，并将筛选器模块返回到已 *分离* 状态。

-   返回 NDIS \_ 状态 \_ 成功或相应的失败代码。 如果驱动程序返回失败代码，NDIS 将终止驱动程序堆栈。

**注意**   注册表可以包含一个标志，该标志指定筛选器模块是可选的。 如果可选筛选器模块不附加，NDIS 不会终止驱动程序堆栈的其余部分。

 

筛选器驱动程序无法发出发送请求，指示接收的数据，发出 OID 请求，或从 *附加* 状态指示状态指示。 在*正在运行和正在**暂停*的状态中支持发送和接收操作。 *暂停*、*重新启动*、*正在运行*和*暂停*状态支持 OID 请求和状态指示。

NDIS 调用 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数来分离 NDIS 附加了 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)的筛选器模块。 有关详细信息，请参阅 [分离筛选器模块](detaching-a-filter-module.md)。

 

