---
title: 筛选器模块 OID 请求
description: 筛选器模块 OID 请求
keywords:
- 筛选器模块 WDK 网络，OID 请求
- 筛选器驱动程序 WDK 网络，OID 请求
- NDIS 筛选器驱动程序 WDK，OID 请求
- Oid WDK 网络，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c57354bbd62c312986b1e55c6b429549aa8a8d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837689"
---
# <a name="filter-module-oid-requests"></a>筛选器模块 OID 请求





NDIS 定义对象标识符 (OID) 值以标识适配器参数，其中包括操作参数，如设备特征、可配置的设置和统计信息。 有关 Oid 的详细信息，请参阅 [NDIS oid](/windows-hardware/drivers/ddi/_netvista/)。

筛选器驱动程序可以查询或设置基础驱动程序的操作参数或筛选过量驱动程序的 OID 请求。

NDIS 还为 NDIS 6.1 和更高版本的筛选器驱动程序提供 [直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md) 。 *直接 OID 请求路径* 支持经常查询或设置的 OID 请求。 例如，IPsec 卸载版本 2 (IPsecv2) 接口为 [OID \_ TCP \_ 任务 \_ IPsec \_ 卸载 \_ V2 \_ 添加 \_ ](./oid-tcp-task-ipsec-offload-v2-add-sa.md) 了用于直接 OID 请求的 SA OID。 直接 OID 请求接口对于 NDIS 驱动程序是可选的。

对于 NDIS 6.81 和更高版本的筛选器驱动程序，NDIS 提供 [同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。 *同步 OID 请求路径* 支持需要不应由筛选器驱动程序（如 [RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) oid）进行排队的同步或 oid 的 oid。 同步 OID 请求接口对于 NDIS 驱动程序是可选的，但如果筛选器驱动程序公布了对 RSSv2 的支持，则这是必需的。

以下主题提供了有关筛选器驱动程序 OID 请求的详细信息：

[在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)

[从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)

[筛选器模块直接 OID 请求](filter-module-direct-oid-requests.md)

[筛选器模块同步 OID 请求](filter-module-synchronous-oid-requests.md)

 

