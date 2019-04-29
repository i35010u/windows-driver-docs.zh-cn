---
title: 将数据包转发到物理网络适配器
description: 将数据包转发到物理网络适配器
ms.assetid: 14A78DB2-6643-471D-97B9-4D8524EC3E73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ddf2fea766c14bfed068fae70ee7dc0dad53ecc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323435"
---
# <a name="forwarding-packets-to-physical-network-adapters"></a>将数据包转发到物理网络适配器


**请注意**  此页面假定您熟悉的信息和关系图中的以下页面：
-   [转发扩展](forwarding-extensions.md)
-   [混合转发](hybrid-forwarding.md)
-   [HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)
-   [HYPER-V 可扩展交换机的概述](overview-of-the-hyper-v-extensible-switch.md)
-   [组合提供程序扩展](teaming-provider-extensions.md)

 

此页介绍了转发扩展的 HYPER-V 可扩展交换机可以向前向基础物理适配器发送的数据包的请求的方式。 一个或多个物理网络适配器可以绑定到可扩展交换机外部网络适配器。

例如，可扩展交换机外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 在主机上，MUX 中间驱动程序本身可以绑定到一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展公开到可扩展交换机团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 如扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

如果已安装并启用了可扩展交换机驱动程序堆栈中转发扩展，它负责使可扩展交换机入口数据路径，它获取每个数据包的转发决策，除非数据包是 NVGRE 数据包。 (有关 NVGRE 数据包的详细信息，请参阅[混合转发](hybrid-forwarding.md)。)根据这些转发的决策，扩展可以添加目标端口的数据包的带外 (OOB) 数据[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 在数据包后已完成的可扩展交换机数据路径，可扩展交换机接口提供了其遍历到指定的目标端口的数据包。

**请注意**  如果未安装或启用转发扩展，可扩展切换本身进行转发的数据包将从传入数据路径获取决策。 开关将目标端口添加到 OOB 数据中的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构之前将转发的数据包可扩展交换机出口数据路径。

 

当转发扩展[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)调用函数时， *NetBufferList*参数包含指向的链接列表的指针[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 每个这些结构指定的入口数据路径从获得一个数据包。 在每个数据包的 OOB 数据内**NET\_缓冲区\_列表**结构，数据中包含目标端口[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构。 扩展插件获得**NDIS\_交换机\_转发\_目标\_数组**结构和它的元素通过调用[ *GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)。

**请注意**  若要提高性能，转发扩展可以调用[ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)函数而不是[ *GetNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598157)若要获取的指针[ **NDIS\_开关\_转发\_目标\_数组** ](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构。 扩展执行此操作如果确定它需要为目标端口的数据包的 OOB 数据中的其他数组元素。 有关详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

 

在每个元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)数组定义目标端口，其格式为[**NDIS\_交换机\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)结构。 此结构包含以下成员：

-   **PortId**成员包含一个值，指定可扩展交换机上的目标端口。

-   **NicIndex**成员指定连接到指定的可扩展交换机端口的网络适配器的索引**PortId**成员。

    有关这些索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

如果转发扩展添加了目标端口连接到外部网络适配器，该扩展可以指定基础物理网络适配器的索引。 例如，通过可扩展交换机团队的 LBFO 支持的组合提供程序作为运行无法扩展。 这允许要平衡流量开销，方法是发送请求转发给团队的其他适配器的扩展。

转发扩展必须在添加或修改时请遵循以下准则[ **NDIS\_交换机\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)结构，以转发发送向基础物理网络适配器的请求：

-   如果**PortId**成员指定连接到的外部网络适配器的可扩展交换机端口，必须设置扩展**NicIndex**成员添加到下列的索引值之一：

    -   如果只有一个物理网络适配器绑定到外部网络适配器，必须设置扩展**NicIndex**成员添加到**NDIS\_交换机\_默认\_NIC\_索引**或其中一个。

    -   如果多个物理网络适配器绑定到外部网络适配器，必须设置扩展**NicIndex**成员为非零的索引值的可扩展交换机团队中的目标网络适配器。

    **请注意**  如果**PortId**成员不指定连接到的外部网络适配器的可扩展交换机端口，必须设置扩展**NicIndex**成员向**NDIS\_交换机\_默认\_NIC\_索引**。

     

-   该扩展已添加的所有数据包的目标端口后，它必须调用[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)入口数据路径上的将数据包转发。

有关如何将目标端口添加到数据包的详细信息，请参阅[将数据包转发到 HYPER-V 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)。

出口数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 





