---
title: 克隆数据包流量
description: 克隆数据包流量
ms.assetid: 6BAE348D-B5BA-4B74-8D9B-79B146427D8C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc9a33e7534e39642cf8f1b4968015836df93c59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525380"
---
# <a name="cloning-packet-traffic"></a>克隆数据包流量


本主题介绍 HYPER-V 可扩展如何切换扩展克隆或重复，数据包并将其注入到可扩展交换机数据路径。 克隆数据包的详细信息，请参阅[克隆 NET\_缓冲区\_列表结构](cloned-net-buffer-list-structures.md)。

**请注意**此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

**请注意**可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

筛选和转发扩展的可扩展交换机可以遵循以下准则将克隆的数据包注入到可扩展交换机入口或出口数据路径：

-   扩展必须首先分配[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)克隆数据包的结构。 扩展必须然后数据包数据将从复制的原始数据包到克隆的数据包。 如何克隆数据包的详细信息，请参阅[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)。

-   扩展分配后[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构，它必须调用[ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)处理程序函数的数据包分配可扩展交换机转发上下文。

    转发上下文驻留在数据包的带外 (OOB) 数据。 它包含转发的数据包，例如其源端口和数组的一个或多个目标端口的信息。

    有关转发上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   扩展必须复制 OOB 数据，包括现有的源端口，从通过调用克隆的数据包的原始数据包[ *CopyNetBufferListInfo*](https://msdn.microsoft.com/library/windows/hardware/hh598136)。 如果该扩展计划要注入的入口数据路径的数据包，它还需要从原始数据包的 OOB 数据复制的目标端口。

    它在复制时的 OOB 数据，该扩展必须遵循以下准则：

    -   如果筛选扩展计划要注入的入口数据路径的数据包，它必须调用[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)与的 NDIS\_开关\_复制\_NBL\_INFO\_标志\_保留\_未指定目标标志。 这将导致原始数据包的目标端口不会复制到克隆的数据包。 时筛选扩展会将此数据包注入到入口数据路径，则目标端口将添加到数据包中的基础的转发扩展 （如果启用驱动程序堆栈中） 或可扩展交换机的微型端口边缘。

    -   如果筛选扩展计划要将数据包注入到出口数据路径，它必须调用[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)与的 NDIS\_开关\_复制\_NBL\_INFO\_标志\_保留\_目标指定的标志。 这将导致原始数据包的目标端口，以复制到克隆的数据包。

-   如果筛选扩展是在克隆或复制的包将从出口数据路径中获取了，它可以更改数据包的目标端口后，它调用[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)与NDIS\_交换机\_副本\_NBL\_信息\_标志\_保留\_目标指定的标志。 此过程的详细信息，请参阅[修改数据包的可扩展交换机的源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

-   如果转发扩展是在克隆或复制的包将从传入数据路径中获取了，它必须先将数据包注入的入口数据路径添加新数据包的目标端口。 此过程的详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

-   扩展调用后[ *CopyNetBufferListInfo*](https://msdn.microsoft.com/library/windows/hardware/hh598136)，数据包将被分配原始数据包中所包含的相同源端口信息。

    该扩展可以调用[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)更改数据包的带外 (OOB) 数据中的源端口信息。

    该扩展可能想要视为源自特定端口的数据包。 这样，该端口将应用于该数据包的策略。 扩展调用[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)更改数据包的源端口。

    但是，可能有该扩展可能会的想要分配到的数据包的源端口标识符**NDIS\_交换机\_默认\_端口\_ID**。 例如，该扩展可能想要将源端口标识符设置为**NDIS\_交换机\_默认\_端口\_ID**为发送到设备的专有控制数据包外部网络。

-   在标准的 NDIS 数据路径中，非可扩展交换机 OOB 数据通常具有不同的值，具体取决于是否指示为发送或接收数据包。 例如， [ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff565812) OOB 数据是发送和接收 – 特定结构的联合

    在可扩展交换机数据路径中，所有数据包移动到每个扩展驱动程序堆栈上为同时发送和接收。 因此，非可扩展交换机 OOB 数据中的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构将在发送或接收的格式通过驱动程序堆栈的流。

    此 OOB 数据的格式取决于源可扩展交换机端口从该数据包到达可扩展交换机。 如果源端口连接到外部网络适配器，非可扩展交换机 OOB 数据将为接收格式。 对于其他端口，此 OOB 数据将发送格式。

    源端口信息存储在[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)数据包的 OOB 数据中联合[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 该扩展使用获取数据[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://msdn.microsoft.com/library/windows/hardware/hh598259)宏。

    **请注意**如果该扩展克隆的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，它必须考虑非可扩展交换机 OOB 数据时，如果它添加或修改 OOB 数据。 该扩展可以调用[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)将 OOB 的所有数据源数据包从复制到克隆的数据包。 此函数将维护 OOB 发送或接收时将数据复制到数据包格式。



-   当扩展克隆一个数据包时，克隆的数据包数据位于本地，或*受信任*，父操作系统的 HYPER-V 父分区中的内存。 此内存不访问的子分区。 因此，它被视为"安全"未同步的更新中由该分区中运行来宾操作系统。

    克隆的原始数据包后，必须获取该扩展[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/hh598211) union 中通过使用克隆的数据包[ **NET\_缓冲区\_列表\_交换机\_转发\_详细信息**](https://msdn.microsoft.com/library/windows/hardware/hh598259)宏。 扩展必须设置**IsPacketDataSafe**成员为 TRUE。 这将指定的所有数据包数据位于受信任的内存中。

筛选和转发扩展必须遵循以下准则，以便将克隆的数据包注入到入口或出口数据路径：

-   扩展必须调用[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)克隆的数据包注入的入口数据路径。 扩展必须设置*SendFlags*使用相应的可扩展交换机标志设置的参数。 有关详细信息，有关这些标志设置，请参阅[HYPER-V 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。

    NDIS 时调用的扩展[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)函数以完成克隆数据包在发送请求，则扩展必须调用[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)以释放已分配的转发上下文。 扩展必须执行此操作之前它释放或重用[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)数据包的结构。

    **请注意**如果修改的数据包，它从出口数据路径获取的数据包数据或源端口扩展必须将克隆的数据包注入到入口数据路径。 它必须将克隆的数据包注入到入口数据路径，如果不保留数据包的目标端口。



-   扩展必须调用[ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820)克隆的数据包注入出口数据路径。 扩展必须设置*ReceiveFlags*使用相应的可扩展交换机标志设置的参数。

    NDIS 时调用的扩展[ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)函数来完成克隆数据包的接收请求，则扩展必须调用[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)它释放或重新使用之前[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构数据包。

    **请注意**转发扩展调用之前[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)，它必须确定克隆的数据包的目标端口和此数据添加到的数据包OOB 数据。



-   如果该扩展克隆的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构，它必须保留的原始数据包的所有权**NET\_缓冲区\_列表**结构直到克隆的数据包的发送或接收请求已完成。 扩展插件必须使用**ParentNetBufferList**克隆数据包的成员**NET\_缓冲区\_列表**要链接到原始数据包的结构**NET\_缓冲区\_列表**结构。

    **请注意**在 NDIS 6.30 (Windows Server 2012)，可以使用该扩展**ParentNetBufferList**成员链接到原始数据包，但它不需要执行此操作。 使用 NDIS 6.40 (Windows Server 2012 R2) 及更高版本，需要扩展**ParentNetBufferList**成员链接到原始数据包。

    一旦克隆的数据包的发送或接收请求已完成，扩展插件必须完成发送或接收的原始数据包的请求。

    **请注意**如果扩展已克隆的数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构，它可以完成此次发送或接收后它的原始数据包的请求克隆。

-   如果该扩展克隆一个数据包，它可以完成此次发送或接收原始数据包的请求，只要进行克隆。

如果转发或筛选扩展获取出口数据路径中的数据包，则它无法插入该数据路径中的数据包的克隆的版本，如果扩展修改数据包数据，或更改源端口。 但是，扩展可以注入这些数据包的入口数据路径。 这允许将数据包转发和正确筛选通过可扩展交换机数据路径。

**请注意**筛选扩展可以仅将注入克隆的数据包的入口数据路径如果数据包的目标端口不会保留。

例如，假定在可扩展交换机出口数据路径中已获取多个目标端口的数据包。 如果一个目标端口需要特殊处理，如数据封装，转发或筛选扩展会处理此通过执行以下步骤：

1.  排除的数据包发送到需要特殊处理的端口。 通过设置的扩展插件实现这**IsExcluded**成员的目标端口[ **NDIS\_开关\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)结构的值。 此过程的详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

2.  克隆的原始数据包并执行所需的数据包数据处理。

    **请注意**筛选扩展不能将克隆的数据包的目标端口添加。 此数据将由转发扩展或可扩展交换机的微型端口边缘稍后添加。

3.  通过调用转发出口数据路径上的原始数据包[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)。

4.  通过调用注入的入口数据路径上的克隆的数据包[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

**请注意**捕获扩展不能克隆数据包流量。 但是，它们可以源自数据包流量。 有关详细信息，请参阅[源自数据包流量](originating-packet-traffic.md)。











