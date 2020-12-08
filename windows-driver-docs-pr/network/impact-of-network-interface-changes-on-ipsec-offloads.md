---
title: 网络接口更改对 IPsec 卸载造成的影响
description: 网络接口更改对 IPsec 卸载造成的影响
keywords:
- 受 ESP 保护的数据包 WDK IPsec 卸载，路由接口已更改
- 受 AH 保护的数据包 WDK IPsec 卸载，路由接口已更改
- 受 ESP 保护的数据包，WDK IPsec 卸载，NIC 被删除，
- 受 AH 保护的数据包，WDK IPsec 卸载，NIC 被删除，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dca97317b6a0c2609f34e515442d24f776e0dfc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801651"
---
# <a name="impact-of-network-interface-changes-on-ipsec-offloads"></a>网络接口更改对 IPsec 卸载造成的影响

\[IPsec 任务卸载功能已弃用，不应使用。\]




网络接口中的以下事件会影响 (IPsec) 任务的卸载 Internet 协议安全：

-   将删除 NIC。

    在将任务卸载到的 NIC 从系统中删除之前，其微型端口驱动程序应删除 NIC (SAs) 的所有安全关联。 微型端口驱动程序无需请求 TCP/IP 传输删除 SAs。

-   路由接口已更改。

    当通过新接口路由网络流量时，TCP/IP 堆栈会临时执行 IPsec 任务，直到将相应的 SAs 添加到新接口中使用的 NIC。 TCP/IP 堆栈通过发出 [OID \_ TCP \_ 任务 " \_ IPSEC \_ 添加 \_ SA](./oid-tcp-task-ipsec-add-sa.md)" 将 SA 添加到 NIC。 当 NIC 上用于旧接口的 SAs 过期后，TCP/IP 传输会发出 [OID TCP 任务 IPSEC 在需要时尽可能多地 \_ \_ \_ \_ 删除 \_ SA](./oid-tcp-task-ipsec-delete-sa.md) ，以请求 NIC 的微型端口驱动程序删除 nic 中的 SAs。

 

