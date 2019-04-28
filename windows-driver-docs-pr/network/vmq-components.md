---
title: VMQ 组件
description: VMQ 组件
ms.assetid: 74BFE4C1-89C2-400D-A915-88552C215251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20641a8518a111dc8202b5bf61b3e281bdfaf54a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338378"
---
# <a name="vmq-components"></a>VMQ 组件





下图显示在操作环境的虚拟机队列 (VMQ) 中的各种组件之间的关系。

![vmq 组件](images/vmqarch.png)

上图说明了以下 VMQ 组件：

<a href="" id="--------network-virtual-service-provider--netvsp-"></a> **网络虚拟服务提供商 (NetVSP)**  
在 HYPER-V 父分区的管理操作系统中运行 NDIS 驱动程序。 此驱动程序提供服务以支持由 HYPER-V 子分区的网络访问。

**请注意**  从 Windows Server 2008 开始，HYPER-V 可扩展交换机组件提供了在来宾操作系统中运行的 NetVSC 组件 NetVSP 支持。 有关此组件的详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

 

<a href="" id="network-virtual-service-client--netvsc-"></a>**网络虚拟服务客户端 (NetVSC)**  
在 HYPER-V 子分区的来宾操作系统中运行 NDIS 驱动程序。 NetVSC 公开主机计算机上的物理网络适配器的虚拟化的视图。 此虚拟化的设备被称为*VM 网络适配器*。

NetVSC 提供了以下功能：

-   网络的 HYPER-V 子分区中的设备功能的支持。

-   通过将消息传递通过虚拟机总线 (VMBus) 访问的物理网络适配器都指向关联 NetVSP 驱动程序。 此驱动程序在 HYPER-V 父分区的管理操作系统中运行。

<a href="" id="--------virtual-machine-bus--------vmbus-"></a> **虚拟机总线 (VMBus)**  
将控件和数据消息传递的 HYPER-V 父级和子级之间分区虚拟通信总线。

**请注意**  HYPER-V 中，子分区也称为是虚拟机 (VM)。

 

<a href="" id="vm-bus-channel"></a>**VM 总线通道**  
中的 HYPER-V 子分区 NetVSC 和 HYPER-V 父分区中的 NetVSP 之间 VMBus 上的通信通道。

<a href="" id="vm-queue"></a>**虚拟机队列**  
一个队列接收的数据。 支持 VMQ 的网络适配器具有数据路由到虚拟机队列的硬件。

<a href="" id="vmq-filter"></a>**VMQ 筛选器**  
若要测试传入的数据筛选器。 支持 VMQ 的网络适配器使用筛选器来测试数据包数据，以便将该数据包分配给队列。

 

 





