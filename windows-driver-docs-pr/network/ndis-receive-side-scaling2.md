---
title: 接收方缩放
description: 接收方缩放
ms.assetid: 380feb24-1f5e-4faa-9c98-1b3c8fdc27cb
keywords:
- 网络驱动程序 WDK，接收方缩放
- 接收方缩放 WDK 网络 NDIS 6.0
- RSS WDK 网络、 NDIS 6.0
- 网络接收处理 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0f7c58b1abeaf677c79cd6a10a825bd4cfb3c0c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378309"
---
# <a name="receive-side-scaling"></a>接收方缩放





接收的方缩放 (RSS) 提高了与多处理器系统上的网络数据处理相关的系统性能。

有关 RSS 的介绍性信息，请参阅[接收方缩放简介](introduction-to-receive-side-scaling.md)。

从 Windows 10，版本 1709，开始 RSS 版本 2 (RSSv2) 是适用于微型端口驱动程序。 基本的 RSS 模型通过提供每个 VPort 分布提升 RSSv2。 有关详细信息，请参阅[接收端缩放版本 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)。 RSSv2 为预览版，仅在 Windows 10 版本 1709年中。

下面的主题介绍可以使用不同级别的硬件和软件支持 RSS 实现：

[非 RSS 接收处理](non-rss-receive-processing.md)

[与单个硬件 RSS 接收队列](rss-with-a-single-hardware-receive-queue.md)

[与硬件队列的 RSS](rss-with-hardware-queuing.md)

[RSS 与消息信号中断](rss-with-message-signaled-interrupts.md)

以下主题提供有关 RSS 的其他信息：

[RSS 哈希算法类型](rss-hashing-types.md)

[RSS 哈希函数](rss-hashing-functions.md)

[验证 RSS 哈希计算](verifying-the-rss-hash-calculation.md)

[RSS 配置](rss-configuration.md)

[设置 RSS CPU 配置](setting-the-rss-cpu-configuration.md)

[RSS 的标准化的 INF 关键字](standardized-inf-keywords-for-rss.md)

[指示 RSS 接收数据](indicating-rss-receive-data.md)

[在中间的驱动程序或筛选器驱动程序中支持 RSS](supporting-rss-in-intermediate-drivers-or-filter-drivers.md)

 

 





