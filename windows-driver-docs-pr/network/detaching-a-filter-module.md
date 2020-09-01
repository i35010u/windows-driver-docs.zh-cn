---
title: 分离筛选器模块
description: 分离筛选器模块
ms.assetid: ef987f2f-a681-4ddb-959a-1becdf633678
keywords:
- 筛选器模块 WDK 网络，分离
- 分离筛选器模块
- 筛选器驱动程序 WDK 网络，分离筛选器模块
- NDIS 筛选器驱动程序 WDK，分离筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c692b8776e0a12b9a98b8ad7571bbf23d16591b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214740"
---
# <a name="detaching-a-filter-module"></a>分离筛选器模块





为了启动从驱动程序堆栈分离筛选器模块的过程，NDIS 调用筛选器驱动程序的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数。 在 *FilterDetach* 函数中的执行开始时，筛选器模块将进入已 *分离* 状态。 分离筛选器模块之前，NDIS 必须暂停驱动程序堆栈。 有关暂停驱动程序堆栈的详细信息，请参阅 [暂停驱动程序堆栈](pausing-a-driver-stack.md)。

在其 *FilterDetach* 函数中，驱动程序将释放其上下文区域和其他资源 (如受影响的筛选器模块) 的缓冲池。 筛选器驱动程序无法对 *FilterDetach*的调用失败。 因此，在附加操作期间，筛选器驱动程序应预分配，以便成功执行分离操作所需的所有资源。 有关附加筛选器模块的详细信息，请参阅 [附加筛选器模块](attaching-a-filter-module.md)。

筛选器模块从 *FilterDetach*返回后，NDIS 可以启动暂停的驱动程序堆栈。 有关启动驱动程序堆栈的详细信息，请参阅 [启动驱动程序堆栈](starting-a-driver-stack.md)。

 

