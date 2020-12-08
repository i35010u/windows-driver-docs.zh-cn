---
title: 更易于编写的筛选器驱动程序
description: 更易于编写的筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 网络，编写筛选器驱动程序
- NDIS 筛选器驱动程序 WDK，编写筛选器驱动程序
- 编写筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5ab530ea98d035d699bcd638a987ae454e202bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822991"
---
# <a name="easier-to-write-filter-drivers"></a>更易于编写的筛选器驱动程序





与上一 NDIS 筛选器中间驱动程序相比，NDIS 6.0 筛选器驱动程序更易于编写。

与筛选器中间驱动程序相比，筛选器驱动程序提供以下实现优势：

-   筛选器驱动程序不包括完整的微型端口驱动程序接口和完整的协议驱动程序接口。

-   筛选器驱动程序不创建和管理虚拟设备。 筛选器驱动程序中没有虚拟小型端口。

-   如果筛选器驱动程序筛选特定服务，则驱动程序可以绕过其他服务。 对于绕过的服务，驱动程序不需要代码。 例如，如果筛选器驱动程序筛选 OID 请求，但不筛选发送和接收操作，则筛选器驱动程序不需要发送和接收入口点。

有关 NDIS 6.0 筛选器驱动程序的详细信息，请参阅 [ndis 6.0 筛选器驱动程序](ndis-filter-drivers.md)。

 

 





