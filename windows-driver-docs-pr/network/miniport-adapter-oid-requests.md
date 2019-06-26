---
title: 微型端口适配器 OID 请求
description: 微型端口适配器 OID 请求
ms.assetid: c3769b1e-c84a-499d-9f93-17a31441a477
keywords:
- Oid WDK 网络、 微型端口适配器请求
- 微型端口适配器 WDK 网络、 OID 请求
- 适配器 WDK 网络、 OID 请求
- 对象标识符 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a442f4eb223c43108279df4ba2d8c77aec267972
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373948"
---
# <a name="miniport-adapter-oid-requests"></a>微型端口适配器 OID 请求





NDIS 定义用于标识微型端口适配器参数，包括操作参数，如设备特征、 可配置的设置和统计信息的对象标识符 (OID) 值。 有关 Oid 的详细信息，请参阅[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

NDIS 6.1 和更高版本的微型端口驱动程序，提供 NDIS[直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)。 *直接 OID 请求路径*支持查询或频繁设置的 OID 请求。 直接 OID 请求接口是可选的 NDIS 驱动程序。

对于 NDIS 6.80 和更高版本的微型端口驱动程序，提供的 NDIS[同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。 *同步 OID 请求路径*支持需要同步的 Oid 或应将排队的筛选器驱动程序，如的 Oid [RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同步 OID 请求接口是可选的 NDIS 驱动程序，但如果微型端口驱动程序播发 RSSv2 的支持是必需的。

以下主题提供有关微型端口驱动程序 OID 请求的详细信息：

[处理中的微型端口适配器 OID 请求](handling-oid-requests-in-a-miniport-adapter.md)

[微型端口适配器 OID 请求序列化](miniport-adapter-oid-request-serialization.md)

[微型端口适配器直接 OID 请求](miniport-adapter-direct-oid-requests.md)

[微型端口适配器同步 OID 请求](miniport-adapter-synchronous-oid-requests.md)
