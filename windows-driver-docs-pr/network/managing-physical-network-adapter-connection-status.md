---
title: 管理物理网络适配器连接状态
description: 管理物理网络适配器连接状态
ms.assetid: B8C6EB48-59D7-469B-87C8-57E60CB5C5D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3fe43016c873817e1f43a94dd59d1f41577ecc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213951"
---
# <a name="managing-physical-network-adapter-connection-status"></a>管理物理网络适配器连接状态


Hyper-v 可扩展交换机体系结构支持与单个外部网络适配器的连接，以访问基础物理介质。 可以使用各种配置将外部网络适配器绑定到一个或多个基础物理网络适配器。 有关这些配置的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

可扩展交换机接口通过以下步骤通知每个物理网络适配器连接状态的扩展：

1.  可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 [oid \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md)的请求。 此 OID 请求通知底层的可扩展交换机扩展，其中介绍了如何创建与可扩展交换机外部网络适配器的网络连接。

    创建网络连接后，将为其分配 NDIS \_ 交换机 \_ NIC \_ 索引值。 此索引值标识可扩展交换机端口上适配器的网络连接。 到外部网络适配器的网络连接分配有 \_ \_ ndis 交换机 nic \_ 索引值 **ndis \_ 交换机 \_ 默认 \_ nic \_ 索引**。

2.  对于直接或间接绑定到外部网络适配器的每个网络适配器，可扩展交换机的协议边缘会发出单独的 OID [ \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md)请求。 此 OID 请求通知扩展有关创建到基础网络适配器的网络连接的信息。

    绑定到外部网络适配器的每个物理网络适配器或虚拟网络适配器都按以下方式分配标识符：

    -   如果将单个物理适配器绑定到外部网络适配器，则会为其分配一个 NDIS \_ 交换机 \_ NIC \_ 索引值为1。

    -   如果负载平衡 (LBFO 的故障转移) 将网络适配器组绑定到外部网络适配器，则会将 NDIS \_ 交换机 \_ NIC \_ 索引值指定为1。

        **注意**  在 LBFO 团队配置中，只会将支持 LBFO 团队的 LBFO 提供程序的虚拟微型端口边缘视为绑定到外部网络适配器。




-   如果将网络适配器的可扩展交换机组绑定到外部网络适配器，则会为该组中的每个物理网络适配器分配一个 \_ \_ 大于或等于1的唯一 NDIS 交换机 NIC \_ 索引值。

    **注意**  在可扩展交换机团队配置中，组中的每个物理网络适配器都被视为绑定到外部网络适配器。




3.  可扩展交换机的协议边缘向外部网络适配器发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md) 的 oid 设置请求。

    **注意**  此时，与外部网络的连接不可操作，并且不能用于数据包通信。



4.  对于绑定到外部网络适配器的每个网络适配器，可扩展交换机的协议边缘会发出单独的 OID [ \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md)请求。 在成功完成 [oid \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md) 的 oid 设置请求后发出此 OID 请求。

    [Oid \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md) OID 请求通知扩展：可扩展交换机网络连接现在可操作。 如果外部网络适配器绑定到 MUX 驱动程序的虚拟微型端口边缘，则协议边缘发出单独的 OID \_ 交换机 \_ NIC \_ CONNECT 请求。

    **注意**  一旦为物理网络适配器（其 NDIS 交换机 nic 索引值大于或等于1）发出 [OID \_ 交换机 \_ nic \_ CONNECT](./oid-switch-nic-connect.md) 请求 \_ ，与 \_ \_ 外部网络的连接就会正常运行。 此时，可以通过外部网络发送或接收数据包通信。



5.  如果外部网络连接被破坏，可扩展交换机的协议边缘首先为绑定到外部网络适配器的每个网络适配器发出 [oid \_ 交换机 \_ NIC \_ ](./oid-switch-nic-disconnect.md) 的单独 oid 请求。 完成这些 OID 请求后，可扩展交换机的协议边缘便会为绑定到外部网络适配器的每个物理网络适配器发出 [oid \_ 交换机 \_ NIC \_ 删除](./oid-switch-nic-delete.md) 的单独 oid 集请求，

    断开连接到基础物理适配器的所有网络连接并将其删除后，可扩展交换机的协议边缘会发出 [oid \_ 交换机 \_ nic \_ Disconnect 断开](./oid-switch-nic-disconnect.md) 连接和 [oid \_ 交换机 \_ nic \_ delete](./oid-switch-nic-delete.md) 请求以断开连接，并删除外部网络适配器连接。

有关 NDIS \_ 交换机 \_ NIC 索引值的详细信息 \_ ，请参阅 [网络适配器索引值](network-adapter-index-values.md)。