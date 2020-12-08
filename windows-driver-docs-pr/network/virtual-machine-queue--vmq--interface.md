---
title: 虚拟机队列 (VMQ) 接口
description: 虚拟机队列 (VMQ) 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de265b1aa1ef81426c37b5dec9f03b56101c457
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802247"
---
# <a name="virtual-machine-queue-vmq-interface"></a>虚拟机队列 (VMQ) 接口


支持 VMQ 接口的网络适配器包括将数据包路由到接收队列的硬件。 这需要在网络适配器上分析数据包标头和队列配置。

当微型端口驱动程序发出接收指示时，所有数据包都适用于同一 VM 队列。

作为一个选项，网络适配器可以在硬件中为指定的媒体访问控制提供 VLAN 筛选 (MAC) 地址。

若要将数据包路由到队列，并将队列中的所有数据包都路由到 VM，则可以为多个 Vm 提供并发接收处理。 每个队列由不同的处理器提供服务。

路由到网络适配器中的队列可阻止复制步骤将数据从网络适配器接收缓冲区复制到 VM 地址空间。

下图显示了 VMQ 接口内的综合数据路径。

![说明包含 vmq 的综合设备数据路径的示意图](images/vmqdatapaths.png)

在图中，物理网络适配器的微型端口驱动程序指示已接收到 Hyper-v 可扩展交换机组件的数据。 此组件充当网络虚拟服务提供商 (NetVSP) ，并提供服务以支持 Hyper-v 子分区的网络访问。

可扩展交换机提供的服务包括在来宾操作系统中的虚拟机 (VM) 网络适配器之间路由数据包。 VM 网络适配器由在来宾操作系统中运行 (Netvsc.sys) 的网络虚拟服务客户端公开。

在 VMQ 下，物理网络适配器会将对 VMQ 的接收筛选器测试匹配的数据直接传输到该队列。 这会阻止在可扩展交换机中进行软件处理。 未通过任何筛选器测试的数据将转到可扩展交换机必须处理数据的默认队列。 除了阻止在可扩展交换机中进行路由和复制以外，还会将 VM 队列的接收中断分配给不同的处理器。

有关 VMQ 接口的详细信息，请参阅 [ (VMQ) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。

 

 





