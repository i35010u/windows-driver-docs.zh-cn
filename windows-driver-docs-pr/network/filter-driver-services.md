---
title: 筛选器驱动程序服务
description: 筛选器驱动程序服务
keywords:
- 筛选器驱动程序 WDK 网络，服务
- NDIS 筛选器驱动程序 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0ae0a87886e1d7865fcf3ddc7664b70688e39ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816601"
---
# <a name="filter-driver-services"></a>筛选器驱动程序服务





筛选器驱动程序可以提供以下服务：

-   发出发送请求和接收指示。

-   在发送和接收数据路径中修改数据缓冲区排序或计时。

-   添加、修改、删除驱动程序堆栈的发送和接收数据路径中的网络数据缓冲区。 有关筛选发送和接收数据的详细信息，请参阅 [筛选模块发送和接收操作](filter-module-send-and-receive-operations.md)。

-   发起查询并设置对底层驱动程序的 OID 请求。

-   筛选查询，并将 OID 请求设置为底层驱动程序。

-   筛选来自基础驱动程序的 OID 请求的响应。 有关 OID 请求的详细信息，请参阅 [筛选器模块 OID 请求](filter-module-oid-requests.md)。

-   对过量驱动程序产生状态指示。

-   来自基础驱动程序的筛选状态指示。 有关详细信息，请参阅 [筛选模块状态指示](filter-module-status-indications.md)。

-   管理其接口的每个微型端口适配器的注册表中的配置参数。 有关详细信息，请参阅 [访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

 

 





