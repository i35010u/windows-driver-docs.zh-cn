---
title: 更快的筛选器驱动程序
description: 更快的筛选器驱动程序
ms.assetid: df708a7d-70e9-4a29-bbd2-4e2b84ed493d
keywords:
- 筛选器驱动程序 WDK 网络 NDIS
- NDIS 筛选器驱动程序 WDK
- 中间驱动程序 WDK 网络，与筛选器驱动程序
- NDIS 中间层驱动程序 WDK、 vs 筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25ae2df670fe092c016e70e9a92c3763e4c2220
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350024"
---
# <a name="faster-filter-drivers"></a>更快的筛选器驱动程序





NDIS 6.x 筛选器驱动程序模型将取代 NDIS 5.x 筛选器中间驱动程序模型。 新的筛选器驱动程序模型增强了系统性能几种方式：

-   与的 NDIS 筛选器中间驱动程序、 NDIS 6.0 或更高版本的筛选器驱动程序组合微型端口驱动程序和协议驱动程序未实现。 它具有一个唯一的接口，类似于微型端口和协议驱动程序，但针对筛选驱动程序堆栈传递的信息进行了优化。

-   NDIS 6.0 和更高版本的筛选器驱动程序支持绕过功能，因此，不需要此类处理时，该驱动程序不会处理数据。

-   NDIS 6.0 和更高版本的筛选器驱动程序可以动态插入或删除从驱动程序堆栈在运行时无需关闭绑定。 执行此类动态操作之前，NDIS 6.0 暂停堆栈中的所有的 NDIS 驱动程序。 NDIS 重新配置完成后，将重新启动堆栈。

NDIS 6.0 筛选器驱动程序有关的详细信息，请参阅[NDIS 6.0 筛选器驱动程序](ndis-filter-drivers.md)。

 

 





