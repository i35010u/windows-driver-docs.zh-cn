---
title: 更快的筛选器驱动程序
description: 更快的筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 网络，NDIS
- NDIS 筛选器驱动程序 WDK
- 中间驱动程序 WDK 网络，vs 筛选器驱动程序
- NDIS 中间驱动程序 WDK，vs 筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd5da867d11e83ba0ea2d09e6bac7894346fc064
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794649"
---
# <a name="faster-filter-drivers"></a>更快的筛选器驱动程序





NDIS 1.x 筛选器驱动程序模型取代了 NDIS 1.x 筛选器中间驱动程序模型。 新的筛选器驱动程序模型通过多种方式增强了系统性能：

-   不同于 NDIS 筛选器中间驱动程序，NDIS 6.0 或更高版本的筛选器驱动程序未作为组合微型端口驱动程序和协议驱动程序实现。 它具有一个与微型端口和协议驱动程序类似的唯一接口，但它已针对筛选器堆栈上传递的筛选信息进行了优化。

-   NDIS 6.0 和更高版本的筛选器驱动程序支持绕过的功能，以便在不需要此类处理时，驱动程序不处理数据。

-   在运行时，可以在运行时将 NDIS 6.0 和更高版本的筛选器驱动程序动态插入或删除，而无需撕裂绑定。 在进行此类动态操作之前，NDIS 6.0 将暂停堆栈中的所有 NDIS 驱动程序。 重新配置完成后，NDIS 将重新启动堆栈。

有关 NDIS 6.0 筛选器驱动程序的详细信息，请参阅 [ndis 6.0 筛选器驱动程序](ndis-filter-drivers.md)。

 

 





