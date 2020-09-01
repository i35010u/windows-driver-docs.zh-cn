---
title: 远程 NDIS 消息传送
description: 远程 NDIS 消息传送
ms.assetid: 6364a9a1-c65f-463d-971b-cf94cd2a5cde
keywords:
- 远程 NDIS WDK 网络，消息传送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf1a9674b9b1d7153ac5dd36d1b2cf350c951af6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207809"
---
# <a name="remote-ndis-messaging"></a>远程 NDIS 消息传送





远程 NDIS 消息分为两种类型： *控制消息* 和 *数据消息*。 控制消息允许主机和远程 NDIS 设备通过通信通道互相通信。 数据消息包含主机与设备之间的通信所需的消息数据信息，并通过数据通道进行通信。

-   **远程 NDIS 控制消息**

    远程 NDIS 控制消息可以由主机发送到远程 NDIS 设备，也可以由远程 NDIS 设备发送到主机。 以下远程 NDIS 控制消息必须受以太网802.3 无连接设备支持：

    [远程 \_ NDIS \_ 初始化 \_ 消息](/previous-versions/ff570624(v=vs.85))

    [远程 \_ NDIS \_ 初始化 \_ CMPLT](/previous-versions/ff570621(v=vs.85))

    [远程 \_ NDIS \_ 停止 \_ 消息](/previous-versions/ff570613(v=vs.85))

    [远程 \_ NDIS \_ 查询 \_ 消息](/previous-versions/ff570641(v=vs.85))

    [远程 \_ NDIS \_ 查询 \_ CMPLT](/previous-versions/ff570638(v=vs.85))

    [远程 \_ NDIS \_ 设置 \_ 消息](/previous-versions/ff570654(v=vs.85))

    [远程 \_ NDIS \_ 设置 \_ CMPLT](/previous-versions/ff570651(v=vs.85))

    [远程 \_ NDIS \_ 重置 \_ 消息](/previous-versions/ff570648(v=vs.85))

    [远程 \_ NDIS \_ 重置 \_ CMPLT](/previous-versions/ff570645(v=vs.85))

    [远程 \_ NDIS \_ 指示 \_ 状态 \_ 消息](/previous-versions/ff570617(v=vs.85))

    [远程 \_ NDIS \_ KEEPALIVE \_ 消息](/previous-versions/ff570629(v=vs.85))

    [远程 \_ NDIS \_ KEEPALIVE \_ CMPLT](/previous-versions/ff570626(v=vs.85))

-   **远程 NDIS 数据消息**

    远程 NDIS 设备必须通过 [远程 \_ ndis \_ 数据包 \_ ](/previous-versions/ff570635(v=vs.85)) 消息结构中包含的远程 ndis 数据包来发送和接收数据。 远程 NDIS 数据包也可能包含带外数据以及跨网络的数据。

    无连接 (例如，802.3) 和面向连接的 (例如，ATM) 设备使用相同的 **远程 \_ NDIS \_ 数据包 \_ ** 消息结构，以便为数据包处理的常见代码提供便利。

 

