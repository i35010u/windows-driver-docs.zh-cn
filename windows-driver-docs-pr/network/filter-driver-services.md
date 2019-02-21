---
title: 筛选器驱动程序服务
description: 筛选器驱动程序服务
ms.assetid: 72ee00c6-0887-46bd-a329-ee7bf0dd2c06
keywords:
- 筛选器驱动程序 WDK 联网服务
- NDIS 筛选器驱动程序 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49042f38727998439dbdbaa008363740a0f7dc8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540407"
---
# <a name="filter-driver-services"></a>筛选器驱动程序服务





筛选器驱动程序可以提供以下服务：

-   源自发送请求和接收的指示。

-   修改数据缓冲区排序或时间设置以发送和接收数据路径。

-   添加、 修改、 删除网络数据缓冲区中的这两个发送和接收数据路径的驱动程序堆栈。 有关筛选的详细信息将发送和接收数据，请参阅[筛选器模块发送和接收操作](filter-module-send-and-receive-operations.md)。

-   源自查询并将 OID 请求设置为基础的驱动程序。

-   筛选查询并将 OID 请求设置为基础的驱动程序。

-   筛选的 OID 请求从基础驱动程序的响应。 有关 OID 的请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

-   源自基础驱动程序的状态指示。

-   从基础驱动程序的状态指示的筛选器。 有关详细信息，请参阅[筛选器模块状态指示](filter-module-status-indications.md)。

-   管理每个与该接口的微型端口适配器的注册表中的配置参数。 有关详细信息，请参阅[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

 

 





