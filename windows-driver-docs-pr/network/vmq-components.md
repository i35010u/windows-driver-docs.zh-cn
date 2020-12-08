---
title: VMQ 组件
description: VMQ 组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f048bd3a764c67d09efd5d0494f2e7ad700fb04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836689"
---
# <a name="vmq-components"></a>VMQ 组件





下图显示了虚拟机队列中各种组件之间的关系 (VMQ) 操作环境。

![vmq 组件](images/vmqarch.png)

上图说明了以下 VMQ 组件：

<a href="" id="--------network-virtual-service-provider--netvsp-"></a>**网络虚拟服务提供商 (NetVSP)**  
在 Hyper-v 父分区的管理操作系统中运行的 NDIS 驱动程序。 此驱动程序提供服务以支持 Hyper-v 子分区对网络的访问。

**注意**  从 Windows Server 2008 开始，Hyper-v 可扩展交换机组件为在来宾操作系统中运行的 Netvsc.sys 组件提供 NetVSP 支持。 有关此组件的详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

 

<a href="" id="network-virtual-service-client--netvsc-"></a>**网络虚拟服务客户端 (Netvsc.sys)**  
在 Hyper-v 子分区的来宾操作系统中运行的 NDIS 驱动程序。 Netvsc.sys 公开主机上物理网络适配器的虚拟化视图。 此虚拟化设备称为 *VM 网络适配器*。

Netvsc.sys 提供以下功能：

-   支持 Hyper-v 子分区中的网络设备功能。

-   通过将消息通过虚拟机总线 (VMBus) 传递到关联的 NetVSP 驱动程序来访问物理网络适配器。 此驱动程序在 Hyper-v 父分区的管理操作系统中运行。

<a href="" id="--------virtual-machine-bus--------vmbus-"></a>**虚拟机总线 (VMBus)**  
在 Hyper-v 父分区和子分区之间传递控制和数据消息的虚拟通信总线。

**注意**  在 Hyper-v 中，子分区也称为虚拟机 (VM) 。

 

<a href="" id="vm-bus-channel"></a>**VM 总线通道**  
在 Hyper-v 子分区中的 Netvsc.sys 与 Hyper-v 父分区中的 NetVSP 之间的之间的通信通道。

<a href="" id="vm-queue"></a>**VM 队列**  
接收的数据的队列。 支持 VMQ 的网络适配器具有将数据路由到 VM 队列的硬件。

<a href="" id="vmq-filter"></a>**VMQ 筛选器**  
用于测试传入数据的筛选器。 支持 VMQ 的网络适配器使用筛选器来测试数据包数据，以便将数据包分配给队列。

 

 





