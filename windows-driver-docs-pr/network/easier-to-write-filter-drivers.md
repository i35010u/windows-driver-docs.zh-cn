---
title: 更轻松写入筛选器驱动程序
description: 更轻松写入筛选器驱动程序
ms.assetid: 77cb7a9a-f823-4dfa-a0fc-11c174f34250
keywords:
- 筛选器驱动程序 WDK 网络，编写筛选器驱动程序
- NDIS 筛选器驱动程序 WDK，编写筛选器驱动程序
- 写入筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e40f2c5695ab020939b1d2b844d679115d174077
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543749"
---
# <a name="easier-to-write-filter-drivers"></a>更轻松写入筛选器驱动程序





NDIS 6.0 筛选器驱动程序是更轻松地编写比旧 NDIS 筛选器中间的驱动程序。

与筛选器中间驱动程序相比，筛选器驱动程序提供以下实现优点：

-   筛选器驱动程序不包括完整的微型端口驱动程序接口和完成协议驱动程序接口。

-   筛选器驱动程序，不要创建和管理虚拟设备。 筛选器驱动程序中没有任何虚拟微型端口。

-   如果筛选器驱动程序特定的服务筛选器，该驱动程序可以绕过其他服务。 该驱动程序不需要的服务，会绕过代码。 例如，如果筛选器驱动程序筛选器 OID 请求但不会筛选发送和接收操作，筛选器驱动程序不会不需要发送和接收入口点。

NDIS 6.0 筛选器驱动程序有关的详细信息，请参阅[NDIS 6.0 筛选器驱动程序](ndis-filter-drivers.md)。

 

 





