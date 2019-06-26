---
title: 虚拟机网络适配器
description: 虚拟机网络适配器
ms.assetid: 8A2A708C-AB43-4D9F-A7CB-2AC4438BCD54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aadc38e75eeb8efdb9a97a3606dcf8723f1d1566
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354490"
---
# <a name="virtual-machine-network-adapters"></a>虚拟机网络适配器


虚拟机 (VM) 网络适配器的 HYPER-V 子分区中运行来宾操作系统中公开。

**请注意**  HYPER-V 中，子分区也称为是 VM。

 

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可能是网络适配器的综合虚拟化 (*合成网络适配器*)。 在这种情况下，在 VM 中运行的网络虚拟服务客户端 (NetVSC) 公开此虚拟网络适配器。 NetVSC 通过虚拟机总线 (VMBus) 将数据包从可扩展交换机端口和接收的转发。

-   VM 网络适配器可以是物理网络适配器的仿真虚拟化 (*仿真的网络适配器*)。 在这种情况下，VM 网络适配器模仿 Intel 网络适配器，并使用硬件仿真转发从可扩展交换机端口和接收的数据包。

下图显示了 VM 网络适配器之间的接口和可扩展切换 NDIS 6.40 (Windows Server 2012 R2) 及更高版本。

![显示模拟的 vm 网络适配器和 ndis 6.40 可扩展交换机之间的接口流程图](images/vswitchvmnic-ndis640.png)

下图显示 VM 网络适配器和可扩展的交换机之间的接口的 NDIS 6.30 (Windows Server 2012)。

![显示模拟的 vm 网络适配器和 ndis 6.30 可扩展交换机之间的接口流程图](images/vswitchvmnic.png)

用户启动的 HYPER-V VM 时，将执行以下步骤：

1.  可扩展交换机的协议边缘发出的一个对象标识符 (OID) 组请求[OID\_切换\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展，为 VM 创建一个端口。

2.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展先前创建的 VM 端口创建 VM 网络适配器的网络连接。

3.  当网络堆栈是否正常运行，并且绑定到 VM 网络适配器时，可扩展交换机的协议边缘会发出的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展的 VM 网络适配器的网络连接已连接并且正常运行。 此时，该扩展可以检查、 注入，并将数据包转发到已连接到 VM 网络适配器的端口。

当用户停止的 HYPER-V VM 时，将执行以下步骤：

1.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知到的 VM 网络适配器的连接，则正在将调用的基础可扩展交换机扩展。

2.  完成所有数据包流量和目标网络连接的 OID 请求后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展，与 VM 网络适配器的连接已适当地销毁并删除。

3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知所用的 VM 网络适配器连接的端口，则在将调用的基础可扩展交换机扩展。

4.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展已销毁并删除 VM 端口。

 

 





