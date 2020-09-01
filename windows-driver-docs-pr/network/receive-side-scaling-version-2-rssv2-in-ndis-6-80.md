---
title: NDIS 6.80 中的接收端缩放版本 2 (RSSv2)
description: '本主题介绍 NDIS 6.80 中的接收方缩放版本 2 (RSSv2) '
ms.assetid: 39FAE4C5-D4AA-4B99-A9B6-82E2D9C86FCC
keywords: NDIS 6.80 中的接收方缩放版本2，NDIS 6.80 中的 RSSv2，接收方缩放版本 2 WDK NDIS 6.80，RSSv2 网络驱动程序 NDIS 6.80
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8599885902ed474290924bd48c20a72c65d0ab6d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214496"
---
# <a name="receive-side-scaling-version-2-rssv2-in-ndis-680"></a>NDIS 6.80 中的接收端缩放版本 2 (RSSv2)

[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

[接收方缩放](./receive-side-scaling-version-2-rssv2-.md) 改善了与处理多处理器系统上的网络数据相关的系统性能。 NDIS 6.80 和更高版本支持 RSS 版本 2 (RSSv2) ，它通过提供 VPort 分散的队列来扩展 RSS。

RSSv2 对其某个 Oid 使用 NDIS 6.80 同步 OID 请求接口。 有关同步 OID 调用的详细信息，请参阅 [NDIS 6.80 中的同步 oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

有关 RSSv2 的详细信息，请参阅 [接收方缩放版本 2 (RSSv2) ](receive-side-scaling-version-2-rssv2-.md)。