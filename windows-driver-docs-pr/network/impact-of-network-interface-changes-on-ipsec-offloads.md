---
title: 网络接口更改对 IPsec 卸载造成的影响
description: 网络接口更改对 IPsec 卸载造成的影响
ms.assetid: 7d1b2bf9-31a9-4fc4-92f3-dc7b5e0277e3
keywords:
- WDK IPsec 卸载受保护的 ESP 数据包，路由接口更改
- WDK IPsec 卸载受保护的 AH 数据包，路由接口更改
- ESP 保护数据包 WDK IPsec 卸载、 删除的 NIC 和
- AH 保护数据包 WDK IPsec 卸载、 删除的 NIC 和
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfa670125e2434df158e1b9340741b1688ca1705
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369201"
---
# <a name="impact-of-network-interface-changes-on-ipsec-offloads"></a>网络接口更改对 IPsec 卸载造成的影响

\[IPsec 任务卸载功能已弃用，不应使用。\]




网络接口中的以下事件影响的 Internet 协议安全 (IPsec) 任务卸载：

-   删除 NIC。

    其微型端口驱动程序从系统中删除任务卸载到 NIC 之前，应该从 NIC 中删除所有安全关联 (Sa) 微型端口驱动程序无需请求 TCP/IP 传输删除 SAs。

-   更改路由的接口。

    通过新界面路由网络流量，TCP/IP 堆栈将暂时执行 IPsec 任务，直到它的相应 SAs 添加到在新界面中使用的 NIC。 TCP/IP 堆栈将 SA 添加到 NIC，通过发出[OID\_TCP\_任务\_IPSEC\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-sa)。 旧界面使用的 NIC 上 SAs 后过期，TCP/IP 传输问题[OID\_TCP\_任务\_IPSEC\_删除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)多少次所需请求 NIC 的微型端口驱动程序从 NIC 中删除该 SAs

 

 





