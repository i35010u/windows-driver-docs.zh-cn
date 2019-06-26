---
title: 远程 NDIS 消息传送
description: 远程 NDIS 消息传送
ms.assetid: 6364a9a1-c65f-463d-971b-cf94cd2a5cde
keywords:
- 远程 NDIS WDK 连接网络、 消息传送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e95adc44b4e0971fc13ab582fd6c5e94daec086
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385837"
---
# <a name="remote-ndis-messaging"></a>远程 NDIS 消息传送





有两种类型的远程 NDIS 消息：*控制消息*并*数据消息*。 控制消息允许通过的信道与彼此进行通信的主机和远程 NDIS 设备。 数据消息包含所需的主机和设备之间的通信的消息数据信息并且通过数据通道通信。

-   **远程 NDIS 控制消息**

    可以将远程 NDIS 控制消息发送到远程 NDIS 设备主机和主机到远程 NDIS 设备。 以太网 802.3 无连接设备必须支持下列远程 NDIS 控制消息：

    [远程\_NDIS\_初始化\_消息](https://docs.microsoft.com/previous-versions/ff570624(v=vs.85))

    [远程\_NDIS\_初始化\_CMPLT](https://docs.microsoft.com/previous-versions/ff570621(v=vs.85))

    [REMOTE\_NDIS\_HALT\_MSG](https://docs.microsoft.com/previous-versions/ff570613(v=vs.85))

    [远程\_NDIS\_查询\_消息](https://docs.microsoft.com/previous-versions/ff570641(v=vs.85))

    [远程\_NDIS\_查询\_CMPLT](https://docs.microsoft.com/previous-versions/ff570638(v=vs.85))

    [REMOTE\_NDIS\_SET\_MSG](https://docs.microsoft.com/previous-versions/ff570654(v=vs.85))

    [REMOTE\_NDIS\_SET\_CMPLT](https://docs.microsoft.com/previous-versions/ff570651(v=vs.85))

    [REMOTE\_NDIS\_RESET\_MSG](https://docs.microsoft.com/previous-versions/ff570648(v=vs.85))

    [REMOTE\_NDIS\_RESET\_CMPLT](https://docs.microsoft.com/previous-versions/ff570645(v=vs.85))

    [远程\_NDIS\_指示\_状态\_消息](https://docs.microsoft.com/previous-versions/ff570617(v=vs.85))

    [REMOTE\_NDIS\_KEEPALIVE\_MSG](https://docs.microsoft.com/previous-versions/ff570629(v=vs.85))

    [REMOTE\_NDIS\_KEEPALIVE\_CMPLT](https://docs.microsoft.com/previous-versions/ff570626(v=vs.85))

-   **远程 NDIS 数据消息**

    远程 NDIS 设备必须发送和接收通过远程 NDIS 数据包中包含的数据[远程\_NDIS\_数据包\_MSG](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))消息结构。 远程 NDIS 数据包还可能包含带外数据，以及放在网络上的数据。

    这两种无连接 （例如，802.3） 和面向连接的网站 （例如 ATM） 设备使用相同**远程\_NDIS\_数据包\_MSG**为了简化常见消息结构，数据包处理的代码。

 

 





