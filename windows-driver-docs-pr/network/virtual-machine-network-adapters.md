---
title: 虚拟机网络适配器
description: 虚拟机网络适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cda9dc7feff3451bdf2c1b09551d44d31152f60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802261"
---
# <a name="virtual-machine-network-adapters"></a>虚拟机网络适配器


虚拟机 (VM) 网络适配器在 Hyper-v 子分区中运行的来宾操作系统中公开。

**注意**  在 Hyper-v 中，子分区也称为 VM。

 

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可以是网络适配器 (合成 *网络* 适配器) 的综合虚拟化。 在这种情况下，VM 中运行的网络虚拟服务客户端 (Netvsc.sys) 将公开此虚拟网络适配器。 Netvsc.sys)  (VMBus，将数据包转发到可扩展交换机端口，并将其从可扩展交换机端口转发。

-   VM 网络适配器可以是物理网络适配器的模拟虚拟化 (*仿真网络适配器*) 。 在这种情况下，VM 网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到可扩展交换机端口并将其从可扩展交换机端口转发。

下图显示了 VM 网络适配器与可扩展交换机 NDIS 6.40 (Windows Server 2012 R2) 及更高版本之间的接口。

![显示模拟 vm 网络适配器与 ndis 6.40 的可扩展交换机之间的接口的流程图](images/vswitchvmnic-ndis640.png)

下图显示了 VM 网络适配器与 NDIS 6.30 (Windows Server 2012) 的可扩展交换机之间的接口。

![显示模拟 vm 网络适配器与 ndis 6.30 的可扩展交换机之间的接口的流程图](images/vswitchvmnic.png)

当用户启动 Hyper-v VM 时，将执行以下步骤：

1.  可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 [oid \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md) 可扩展交换机驱动程序堆栈的请求。 此 OID 请求通知底层的可扩展交换机扩展：正在为 VM 创建端口。

2.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 集请求，并按可扩展交换机驱动程序堆栈进行创建。 此 OID 请求通知底层的可扩展交换机扩展正在为之前创建的 VM 端口创建 VM 网络适配器的网络连接。

3.  当网络堆栈运行并且已绑定到 VM 网络适配器时，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 设置请求，即关闭可扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展： VM 网络适配器的网络连接已连接并且可操作。 此时，扩展可以检查并注入数据包，并将数据包转发到连接到 VM 网络适配器的端口。

当用户停止 Hyper-v VM 时，会执行以下步骤：

1.  可扩展交换机的协议边缘发出 oid 交换机 NIC 的 OID 集请求断开可扩展交换机驱动程序堆栈的 [ \_ \_ \_ 连接](./oid-switch-nic-disconnect.md) 。 此 OID 请求通知底层的可扩展交换机扩展与 VM 网络适配器的连接被破坏。

2.  在所有针对网络连接的数据包流量和 OID 请求都完成之后，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-port-create.md) 的 oid 设置请求。 此 OID 请求通知底层的可扩展交换机扩展，指出已正确地断开和删除与 VM 网络适配器的连接。

3.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md) 的 oid 集请求，并向下扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展，用于 VM 网络适配器连接的端口正在被破坏。

4.  可扩展交换机的协议边缘向下扩展了 oid [ \_ 交换机 \_ 端口 \_ 删除](./oid-switch-port-delete.md) 扩展交换机驱动程序堆栈的请求。 此 OID 请求通知底层的可扩展交换机扩展 VM 端口已断开并被删除。

 

