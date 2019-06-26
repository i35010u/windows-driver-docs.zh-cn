---
title: 筛选器模块 OID 请求
description: 筛选器模块 OID 请求
ms.assetid: 6de5ec1c-8e12-4f50-8708-ec136cafd9c2
keywords:
- 筛选器模块 WDK 网络、 OID 请求
- 筛选器驱动程序 WDK 网络、 OID 请求
- NDIS 筛选器驱动程序 WDK，OID 请求
- Oid WDK 网络筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6790c6a0d69d52131f50747b0ab3e800d1fed5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363406"
---
# <a name="filter-module-oid-requests"></a>筛选器模块 OID 请求





NDIS 定义用于标识适配器参数，包括操作参数，如设备特征、 可配置的设置和统计信息的对象标识符 (OID) 值。 有关 Oid 的详细信息，请参阅[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

筛选器驱动程序可以查询或设置操作参数的基础驱动程序或筛选的过量驱动程序的 OID 请求。

此外提供了 NDIS [NDIS 6.1 的直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)和更高版本筛选器驱动程序。 *直接 OID 请求路径*支持查询或频繁设置的 OID 请求。 例如，IPsec 卸载版本 2 (IPsecv2) 接口提供了[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)直接 OID 请求的 OID。 直接 OID 请求接口是可选的 NDIS 驱动程序。

对于 NDIS 6.81 和更高版本的筛选器驱动程序，提供的 NDIS[同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。 *同步 OID 请求路径*支持需要同步的 Oid 或应将排队的筛选器驱动程序，如的 Oid [RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同步 OID 请求接口是可选的 NDIS 驱动程序，但如果筛选器驱动程序播发 RSSv2 的支持是必需的。

以下主题提供有关筛选器驱动程序 OID 请求的详细信息：

[NDIS 筛选器驱动程序中的筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)

[NDIS 筛选器驱动程序从生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)

[筛选模块直接 OID 请求](filter-module-direct-oid-requests.md)

[筛选模块同步 OID 请求](filter-module-synchronous-oid-requests.md)

 

 





