---
title: NDIS 6.80 中的接收端缩放版本 2 (RSSv2)
description: 本主题介绍 NDIS 6.80 中的接收方缩放版本2（RSSv2）
ms.assetid: 39FAE4C5-D4AA-4B99-A9B6-82E2D9C86FCC
keywords: NDIS 6.80 中的接收方缩放版本2，NDIS 6.80 中的 RSSv2，接收方缩放版本 2 WDK NDIS 6.80，RSSv2 网络驱动程序 NDIS 6.80
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: baef3583517d6490ce6d8661c7be10617f370504
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210811"
---
[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

# <a name="receive-side-scaling-version-2-rssv2-in-ndis-680"></a>NDIS 6.80 中的接收端缩放版本 2 (RSSv2)

[接收方缩放](ndis-receive-side-scaling2.md)改善了与处理多处理器系统上的网络数据相关的系统性能。 NDIS 6.80 和更高版本支持 RSS 版本2（RSSv2），该版本通过提供按 VPort 分配的队列来扩展 RSS。

RSSv2 对其某个 Oid 使用 NDIS 6.80 同步 OID 请求接口。 有关同步 OID 调用的详细信息，请参阅[NDIS 6.80 中的同步 oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

有关 RSSv2 的详细信息，请参阅[接收方缩放版本2（RSSv2）](receive-side-scaling-version-2-rssv2-.md)。

