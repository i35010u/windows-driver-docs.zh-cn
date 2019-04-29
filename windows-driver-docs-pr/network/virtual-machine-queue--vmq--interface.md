---
title: 虚拟机队列 (VMQ) 接口
description: 虚拟机队列 (VMQ) 接口
ms.assetid: AE0F65F0-7A5B-48FA-8635-617E71D86479
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5caf6ae4646b3baee1bbd0b877b71e779d5d87b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378228"
---
# <a name="virtual-machine-queue-vmq-interface"></a>虚拟机队列 (VMQ) 接口


支持 VMQ 接口的网络适配器包括路由数据包接收队列的硬件。 这需要分析数据包标头和配置网络适配器上的队列。

当微型端口驱动程序的接收指示时，所有数据包是相同的虚拟机队列。

作为一个选项，网络适配器可提供筛选中指定的介质访问控制 (MAC) 地址的硬件的 VLAN。

数据包路由到队列并指示所有队列到 VM 上的数据包允许并发接收多个 Vm 的处理。 每个队列是由不同处理器提供服务。

路由到的网络适配器中的队列会阻止复制步骤，若要复制的网络适配器中的数据接收到 VM 的地址空间的缓冲区。

下图显示 VMQ 界面中使用的综合数据路径。

![说明使用 vmq 的合成设备数据路径的关系图](images/vmqdatapaths.png)

在图中，物理网络适配器的微型端口驱动程序指示最多的 HYPER-V 可扩展交换机组件接收到的数据。 此组件充当网络虚拟服务提供商 (NetVSP)，并提供了用于通过 HYPER-V 子分区来支持网络访问服务。

可扩展交换机提供的服务中的来宾操作系统包括到和从虚拟机 (VM) 网络适配器的路由数据包。 通过在来宾操作系统中运行的网络虚拟服务客户端 (NetVSC) 公开服务的 VM 网络适配器。

下 VMQ，物理网络适配器的接收筛选器测试匹配对 VMQ 直接到该队列将数据传输。 这可以防止在可扩展的交换机中处理的软件。 不传递任何筛选器测试的数据都移动到默认队列其中可扩展交换机必须处理的数据。 除了防止路由和可扩展的交换机中的复制，VM 队列的接收中断将分配给不同的处理器。

VMQ 接口的详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。

 

 





