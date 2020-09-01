---
title: 微型端口适配器 OID 请求
description: 微型端口适配器 OID 请求
ms.assetid: c3769b1e-c84a-499d-9f93-17a31441a477
keywords:
- Oid WDK 网络，微型端口适配器请求
- 小型端口适配器 WDK 网络，OID 请求
- 适配器 WDK 网络，OID 请求
- 对象标识符 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 688f932dc97838350314fc9f18e7ec7461bff0f2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218009"
---
# <a name="miniport-adapter-oid-requests"></a>微型端口适配器 OID 请求





NDIS 定义对象标识符 (OID) 值以标识微型端口适配器参数，其中包括操作参数，如设备特征、可配置的设置和统计信息。 有关 Oid 的详细信息，请参阅 [NDIS oid](/windows-hardware/drivers/ddi/_netvista/)。

对于 NDIS 6.1 和更高的微型端口驱动程序，NDIS 提供 [直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)。 *直接 OID 请求路径*支持经常查询或设置的 OID 请求。 直接 OID 请求接口对于 NDIS 驱动程序是可选的。

对于 NDIS 6.80 和更高的微型端口驱动程序，NDIS 提供 [同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。 *同步 OID 请求路径*支持需要不应由筛选器驱动程序（如[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) oid）进行排队的同步或 oid 的 oid。 同步 OID 请求接口对于 NDIS 驱动程序是可选的，但如果微型端口驱动程序公布了对 RSSv2 的支持

以下主题提供了有关微型端口驱动程序 OID 请求的详细信息：

[处理微型端口适配器中的 OID 请求](handling-oid-requests-in-a-miniport-adapter.md)

[微型端口适配器 OID 请求序列化](miniport-adapter-oid-request-serialization.md)

[微型端口适配器直接 OID 请求](miniport-adapter-direct-oid-requests.md)

[微型端口适配器同步 OID 请求](miniport-adapter-synchronous-oid-requests.md)