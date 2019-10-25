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
ms.openlocfilehash: 0d08ba32725bf073f7640336b582b9bf30c14cc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844250"
---
# <a name="miniport-adapter-oid-requests"></a>微型端口适配器 OID 请求





NDIS 定义对象标识符（OID）值以标识微型端口适配器参数，其中包括操作参数，如设备特征、可配置的设置和统计信息。 有关 Oid 的详细信息，请参阅[NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

对于 NDIS 6.1 和更高的微型端口驱动程序，NDIS 提供[直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)。 *直接 OID 请求路径*支持经常查询或设置的 OID 请求。 直接 OID 请求接口对于 NDIS 驱动程序是可选的。

对于 NDIS 6.80 和更高的微型端口驱动程序，NDIS 提供[同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。 *同步 OID 请求路径*支持需要不应由筛选器驱动程序（如[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) oid）进行排队的同步或 oid 的 oid。 同步 OID 请求接口对于 NDIS 驱动程序是可选的，但如果微型端口驱动程序公布了对 RSSv2 的支持

以下主题提供了有关微型端口驱动程序 OID 请求的详细信息：

[在微型端口适配器中处理 OID 请求](handling-oid-requests-in-a-miniport-adapter.md)

[微型端口适配器 OID 请求序列化](miniport-adapter-oid-request-serialization.md)

[小型端口适配器直接 OID 请求](miniport-adapter-direct-oid-requests.md)

[微型端口适配器同步 OID 请求](miniport-adapter-synchronous-oid-requests.md)
