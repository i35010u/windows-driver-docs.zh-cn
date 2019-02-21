---
title: 在中间的驱动程序或筛选器驱动程序中支持 RSS
description: 在中间的驱动程序或筛选器驱动程序中支持 RSS
ms.assetid: 5e1bfbb0-0b7a-4a9d-a228-4089f7208880
keywords:
- 接收方缩放 WDK 网络连接、 中间驱动程序
- RSS WDK 网络连接、 中间驱动程序
- 接收方缩放 WDK 网络，筛选器驱动程序
- RSS WDK 网络、 筛选器驱动程序
- 筛选器驱动程序 WDK RSS
- 中间驱动程序 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43374f491a5540a6dfc23e609effca7fc8f8e621
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526953"
---
# <a name="supporting-rss-in-intermediate-drivers-or-filter-drivers"></a>在中间的驱动程序或筛选器驱动程序中支持 RSS





所有中间驱动程序和筛选器驱动程序应该至少传递 OID 请求、 其他请求和状态的指示。 中间驱动程序或筛选器驱动程序应提供其他驱动程序特定支持接收方缩放 (RSS) 如果驱动程序执行以下任一项：

-   之后，发送请求。

-   源自接收的指示。

-   队列将请求发送或接收供以后处理的迹象。

跳过发送和接收处理的筛选器驱动程序不需要执行其他任何组件即可支持 RSS。 有关发送或接收请求筛选器驱动程序中有关跳过的详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

QoS 计划程序是应支持 RSS 的筛选器驱动程序的示例。 这类驱动程序队列发送适当的时候发送的数据包。 筛选器驱动程序应使用给定的连接协议驱动程序使用同一个 CPU。

中间驱动程序或不支持 RSS 的筛选器驱动程序可以截获 RSS OID 请求并通过报告不支持 RSS 禁用 RSS。

筛选器驱动程序或中间支持 RSS 的驱动程序可以使用从 RSS Oid 信息要将连接分配到相同的 Cpu 使用的协议驱动程序和微型端口驱动程序。

有关 RSS Oid 的详细信息，请参阅[RSS 配置](rss-configuration.md)。

 

 





