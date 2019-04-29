---
title: 发起数据包流量
description: 发起数据包流量
ms.assetid: 613C7E82-387D-47AE-A699-A799087D3C1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed5afb14e21e4d99530bc5496e6980ed4924eb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378245"
---
# <a name="originating-packet-traffic"></a>发起数据包流量


本主题介绍如何 HYPER-V 扩展发起新的数据包，并将其注入到可扩展交换机数据路径。

**请注意**  此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

 

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*. 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

 

可扩展的交换机扩展可以仅将新的数据包注入到可扩展交换机入口数据路径。 这可确保可扩展交换机接口，可以筛选并正确转发这些数据包。 扩展必须遵循以下准则，以便将新的数据包注入到入口数据路径：

-   扩展必须首先分配[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)新数据包的结构。

-   扩展分配后[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构对于新的数据包，必须调用[ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)处理程序函数的数据包分配可扩展交换机转发上下文。

    转发上下文驻留在数据包的带外 (OOB) 数据。 它包含转发的数据包，例如其源端口和数组的一个或多个目标端口的信息。

    有关转发上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   扩展调用后[ *AllocateNetBufferListForwardingContext*](https://msdn.microsoft.com/library/windows/hardware/hh598134)，该数据包的源端口将设置为**NDIS\_开关\_默认\_端口\_ID**。 源端口标识符的数据包**NDIS\_切换\_默认\_端口\_ID**是受信任并跳过的可扩展交换机端口策略，如访问控制列表 (Acl) 和服务质量 (QoS)。

    该扩展可能想要视为源自特定端口的数据包。 这样，该端口将应用于该数据包的策略。 扩展调用[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)更改数据包的源端口。

    但是，可能有该扩展可能会的想要分配到的数据包的源端口标识符**NDIS\_交换机\_默认\_端口\_ID**。 例如，该扩展可能想要将源端口标识符设置为**NDIS\_交换机\_默认\_端口\_ID**为发送到设备的专有控制数据包外部网络。

-   如果转发扩展的入口数据路径上发送新的数据包，它必须确定数据包的目标端口。 此过程的详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

    **请注意**  捕获或筛选扩展不能将新的目标端口添加到新的数据包。

     

-   当扩展创建新的数据包时，数据包数据位于本地，或*受信任*，父操作系统的 HYPER-V 父分区中的内存。 此内存不可访问的子分区。 因此，它被视为"安全"未同步的更新中由该分区中运行来宾操作系统。

    扩展必须获取[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)通过使用新的数据包的联合[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://msdn.microsoft.com/library/windows/hardware/hh598259)宏。 扩展必须设置**IsPacketDataSafe**成员为 TRUE。 这将指定的所有数据包数据位于受信任的内存中。

-   当扩展调用[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)若要将数据包注入到入口数据路径，它必须设置*标志*参数与相应的可扩展切换标志设置。 有关详细信息，有关这些标志设置，请参阅[HYPER-V 可扩展交换机发送和接收标志](hyper-v-extensible-switch-send-and-receive-flags.md)。

-   NDIS 时调用的扩展[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)函数以完成新数据包在发送请求，则扩展必须调用[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)以释放已分配的转发上下文。 扩展必须执行此操作之前它释放或重用[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568389)数据包的结构。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 





