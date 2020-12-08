---
title: 在中间驱动程序或筛选器驱动程序中支持 RSS
description: 在中间驱动程序或筛选器驱动程序中支持 RSS
keywords:
- 接收方缩放 WDK 网络，中间驱动程序
- RSS WDK 网络，中间驱动程序
- 接收方缩放 WDK 网络，筛选器驱动程序
- RSS WDK 网络，筛选器驱动程序
- 筛选器驱动程序 WDK RSS
- 中间驱动程序 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2df3254193a195ad735fcaf52c9097e9cba77675
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841161"
---
# <a name="supporting-rss-in-intermediate-drivers-or-filter-drivers"></a>在中间驱动程序或筛选器驱动程序中支持 RSS





所有中间驱动程序和筛选器驱动程序至少应传递 OID 请求、其他请求和状态指示。 中间驱动程序或筛选器驱动程序应为接收方缩放提供额外的特定于驱动程序的支持 (RSS) 如果驱动程序执行以下任一操作：

-   发起发送请求。

-   源自接收指示。

-   队列发送请求或接收指示以便以后处理。

绕过发送和接收处理的筛选器驱动程序无需执行任何其他操作即可支持 RSS。 有关跳过筛选器驱动程序中的发送或接收请求的详细信息，请参阅 [数据绕过模式](data-bypass-mode.md)。

QoS 计划程序是应支持 RSS 的筛选器驱动程序的一个示例。 此类驱动程序在适当的时间发送用于发送的数据包。 筛选器驱动程序应使用协议驱动程序为给定连接使用的同一个 CPU。

不支持 RSS 的中间驱动程序或筛选器驱动程序可以通过报告不支持 rss 来截获 RSS OID 请求并禁用 RSS。

支持 RSS 的筛选器驱动程序或中间驱动程序可以使用 RSS Oid 中的信息将连接分配到协议驱动程序和微型端口驱动程序所使用的相同 Cpu。

有关 RSS Oid 的详细信息，请参阅 [Rss 配置](rss-configuration.md)。

 

 





