---
title: 分离筛选器模块
description: 分离筛选器模块
ms.assetid: ef987f2f-a681-4ddb-959a-1becdf633678
keywords:
- 筛选器模块 WDK 连接网络、 分离
- 分离筛选器模块
- 筛选器驱动程序 WDK 网络分离筛选器模块
- NDIS 筛选器驱动程序 WDK，分离筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b1f61ee168262c4a1cb44d945ba8028a286e90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381438"
---
# <a name="detaching-a-filter-module"></a>分离筛选器模块





若要启动分离驱动程序堆栈提供的筛选器模块的过程，NDIS 调用筛选器驱动程序[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)函数。 在中执行的起始*FilterDetach*函数，筛选器模块进入*Detached*状态。 分离筛选器模块之前, NDIS 必须暂停驱动程序堆栈。 有关暂停的驱动程序堆栈的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

在其*FilterDetach*函数，该驱动程序释放其上下文区域和其他资源 （如缓冲池） 的受影响的筛选器模块。 筛选器驱动程序不能对调用进行故障*FilterDetach*。 因此，筛选器驱动程序应预分配，在附加操作期间已成功执行分离操作所需的所有资源。 有关附加筛选器模块的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。

从模块返回的筛选器后*FilterDetach*，NDIS 可以启动暂停的驱动程序堆栈。 有关启动驱动程序堆栈的详细信息，请参阅[启动驱动程序堆栈](starting-a-driver-stack.md)。

 

 





