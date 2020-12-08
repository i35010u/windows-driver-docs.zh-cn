---
title: 内部网络适配器
description: 内部网络适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee873de7eafa232fc7b4a623842ee838f4cbf484
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817121"
---
# <a name="internal-network-adapters"></a>内部网络适配器


内部网络适配器在 Hyper-v 父分区中运行的管理操作系统中公开。 此类型的网络适配器为在管理操作系统中运行的进程提供对可扩展交换机的访问。 这允许这些进程通过可扩展交换机发送或接收数据包。

如果将可扩展交换机配置为提供内部网络适配器连接，则在启动交换机时，将执行以下步骤：

1.  可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 [oid \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md) 可扩展交换机驱动程序堆栈的请求。 此 OID 请求通知底层可扩展交换机扩展：正在为内部网络适配器创建端口

2.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 集请求，并按可扩展交换机驱动程序堆栈进行创建。 此 OID 请求通知底层的可扩展交换机扩展正在为先前创建的端口创建内部网络适配器的网络连接。

3.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 集请求，并沿可扩展交换机驱动程序堆栈向下连接。 此 OID 请求通知底层的可扩展交换机扩展，内部网络适配器的网络连接已连接并且可操作。 此时，扩展可以检查并注入数据包，并将数据包转发到连接到内部网络适配器的端口。

当具有内部网络适配器连接的可扩展交换机停止时，将执行以下步骤：

1.  可扩展交换机的协议边缘发出 oid 交换机 NIC 的 OID 集请求断开可扩展交换机驱动程序堆栈的 [ \_ \_ \_ 连接](./oid-switch-nic-disconnect.md) 。 此 OID 请求通知底层的可扩展交换机扩展，指出与外部网络适配器的连接被破坏。

2.  在所有针对网络连接的数据包流量和 OID 请求都完成之后，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 设置请求。 此 OID 请求通知底层的可扩展交换机扩展已正确地断开和删除与外部网络适配器的连接。

3.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md) 的 oid 集请求，并向下扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展，此端口用于外部网络适配器连接。

4.  可扩展交换机的协议边缘向下扩展了 oid [ \_ 交换机 \_ 端口 \_ 删除](./oid-switch-port-delete.md) 扩展交换机驱动程序堆栈的请求。 此 OID 请求通知底层的可扩展交换机扩展，用于内部网络适配器连接的端口已被断开并被删除。

 

