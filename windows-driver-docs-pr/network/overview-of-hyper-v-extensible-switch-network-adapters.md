---
title: Hyper-V 可扩展交换机网络适配器概述
description: Hyper-V 可扩展交换机网络适配器概述
ms.assetid: 61403FDE-90BF-4D0A-83E1-5AF8ADBD37A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19e137888c50a8bba8d7f45dfd9ce7ae8fb98b9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380685"
---
# <a name="overview-of-hyper-v-extensible-switch-network-adapters"></a>Hyper-V 可扩展交换机网络适配器概述


HYPER-V 可扩展交换机支持各种类型的虚拟或物理网络适配器中的连接。 与这些类型的网络适配器的连接由通过可扩展交换机端口。 虚拟网络适配器连接建立后，并连接的网络适配器，则将调用后，将删除之前创建端口。

例如，当启动 HYPER-V 子分区时，可扩展交换机接口创建端口之前在来宾操作系统中公开的虚拟机 (VM) 网络适配器。 公开和枚举的 VM 网络适配器后，可扩展交换机接口用于创建 VM 网络适配器和可扩展的交换机端口之间的网络连接。 如果子分区已停止，可扩展交换机接口删除网络连接，，然后删除可扩展交换机端口。

HYPER-V 可扩展交换机支持从以下类型的虚拟网络适配器的连接：

<a href="" id="external-network-adapters"></a>外部网络适配器  
这是在 HYPER-V 父分区中运行管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机支持只能有一个外部网络适配器连接。

外部网络适配器提供了与主机上可用的物理网络接口的连接。 可以通过 HYPER-V 父分区和所有子分区访问外部网络适配器。

有关此类型的网络适配器的详细信息，请参阅[外部的网络适配器](external-network-adapters.md)。

<a href="" id="internal-network-adapters"></a>内部网络适配器  
这是在 HYPER-V 父分区中运行管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机支持只能有一个内部网络适配器连接。

内部网络适配器提供对可扩展交换机的管理操作系统中运行的进程的访问。 这允许这些进程发送或接收通过可扩展交换机的数据包。

有关此类型的网络适配器的详细信息，请参阅[内部网络适配器](internal-network-adapters.md)。

<a href="" id="virtual-machine--vm--network-adapters"></a>虚拟机 (VM) 网络适配器  
这是可扩展交换机网络适配器的 HYPER-V 子分区中运行来宾操作系统中公开的。

**请注意**  HYPER-V 中，子分区也称为是 VM。

 

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可能是网络适配器的综合虚拟化 (*合成网络适配器*)。 在这种情况下，在 VM 中运行的网络虚拟服务客户端 (NetVSC) 公开此虚拟网络适配器。 NetVSC 通过虚拟机总线 (VMBus) 将数据包从可扩展交换机端口和接收的转发。

-   VM 网络适配器可以是物理网络适配器的仿真虚拟化 (*仿真的网络适配器*)。 在这种情况下，VM 网络适配器模仿 Intel 网络适配器，并使用硬件仿真转发从可扩展交换机端口和接收的数据包。

有关此类型的网络适配器的详细信息，请参阅[虚拟机网络适配器](virtual-machine-network-adapters.md)。

可扩展交换机的网络适配器连接是创建、 更新和删除通过以下可扩展交换机 OID 请求：

<a href="" id="oid-switch-nic-create"></a>[OID\_交换机\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)以通知有关的网络适配器连接创建可扩展的交换机扩展到可扩展交换机端口。 端口必须之前已创建通过 OID 集请求的[OID\_交换机\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)。

[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)请求仅向扩展新的可扩展交换机网络适配器连接时，要将启动，该数据包流量可能很快就会开始出现通知通过指定端口。

该扩展可以通过返回状态来禁止创建通知\_数据\_不\_OID 请求被接受。 例如，如果扩展不能满足其用于连接的网络适配器的端口上配置的策略，该扩展应能阻止创建通知。

如果扩展接受创建通知，它必须转发 OID 请求下可扩展交换机驱动程序堆栈。 扩展监视此 OID 请求以确定基础扩展是否已被否决创建通知的完成状态。

创建网络适配器连接时，它分配 NDIS\_交换机\_NIC\_索引值。 此索引值标识的可扩展交换机端口上的网络适配器连接。 连接到外部、 内部和 VM 网络适配器分配 NDIS\_交换机\_NIC\_索引值**NDIS\_开关\_默认\_NIC\_索引**。 每个绑定到外部网络适配器的物理或虚拟网络适配器分配 NDIS\_交换机\_NIC\_索引值，如下所示：

-   如果物理或虚拟网络适配器直接绑定到外部网络适配器，则会分配 NDIS\_交换机\_NIC\_之一的索引值。

-   如果物理网络适配器是一个可扩展交换机团队的一部分，则会分配 NDIS\_切换\_NIC\_大于或等于 1 的索引值。 可扩展交换机团队是团队的一个或多个物理网络适配器绑定到可扩展交换机外部网络适配器的配置。

有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

有关详细信息 NDIS\_交换机\_NIC\_索引值，请参阅[网络适配器索引值](network-adapter-index-values.md)。

**请注意**  的扩展插件不能生成或直到可扩展交换机的协议边缘颁发的 OID 集请求通过网络适配器连接转发数据包[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)。

 

<a href="" id="oid-switch-nic-connect"></a>[OID\_交换机\_NIC\_连接](https://msdn.microsoft.com/library/windows/hardware/hh598262)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)通知可扩展交换机扩展，可扩展交换机的网络适配器连接是完全正常运行。

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

OID 后请求已完成，但 NDIS\_状态\_成功、 网络适配器连接和可扩展的交换机端口都是完全正常运行。 此状态的网络适配器连接时，该扩展可以执行以下操作：

-   生成或数据包将流量转发到端口的网络适配器连接。

-   问题可扩展切换 Oid 或用作源端口使用的端口的状态指示。

-   调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增引用计数器，用于连接的网络适配器。 可扩展交换机接口将拆开网络适配器连接，而引用计数器的非零值。

<a href="" id="oid-switch-nic-updated"></a>[OID\_交换机\_NIC\_已更新](https://msdn.microsoft.com/library/windows/hardware/hh846216)  
可扩展交换机的协议边缘发出 OID 集请求的 OID\_切换\_NIC\_经过更新以通知可扩展交换机扩展，已更新的可扩展交换机的网络适配器的参数。 只能将 Nic 已连接，但尚未开始断开连接进程发出 OID。 这些运行时配置更改可以包括*NicFriendlyName*， *MTU*， *NetCfgInstanceId*， *PermanentMacAddress*，*VMMacAddress*， *CurrentMacAddress*，和*VFAssigned。*

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

<a href="" id="oid-switch-nic-disconnect"></a>[OID\_交换机\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)通知可扩展交换机扩展，可扩展交换机的网络适配器连接被销毁。 连接已完全销毁后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)。

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

该扩展将转发此 OID 请求后，不再可以生成或将数据包转发到其连接的网络适配器，则正在将调用的端口。 此外，该扩展不再可以调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)为网络适配器连接。

<a href="" id="oid-switch-nic-delete"></a>[OID\_交换机\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)通知可扩展交换机扩展，可扩展交换机的网络适配器在拆解连接并将其删除。 此 OID 请求时，才发出一个 OID 为其设置的请求的网络连接[OID\_交换机\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)以前颁发。

**请注意**  扩展必须始终转发可扩展交换机在驱动程序堆栈的下层此 OID 集请求。 扩展必须不会使请求失败。

 

完成此 OID 请求后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://msdn.microsoft.com/library/windows/hardware/hh598279)启动删除过程已端口用于连接的网络适配器。

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

可扩展交换机接口维护已创建每个网络适配器连接的引用计数器。 如果它的引用计数器具有非零值，将不会删除网络适配器连接。 接口提供以下处理程序函数，用于递增或递减的可扩展交换机的网络适配器连接的引用计数器：

<a href="" id="referenceswitchnic"></a>[*ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)  
可扩展交换机扩展将调用此函数可使网络适配器连接的引用计数器递增。 尽管引用计数器具有一个非零值，但可扩展交换机接口不会删除网络适配器连接。

该扩展应调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)之前执行以下操作：

-   转发[OID\_切换\_NIC\_请求](https://msdn.microsoft.com/library/windows/hardware/hh598266)可扩展交换机为基础的外部适配器在驱动程序堆栈的下层的请求。

-   转发[ **NDIS\_状态\_切换\_NIC\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598205)状态指示可扩展交换机驱动程序堆栈上从基础外部适配器。

**请注意**  不能调用该扩展[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)的网络适配器连接后接收 OID 设置请求的[OID\_交换机\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)为该连接。

 

<a href="" id="dereferenceswitchnic"></a>[*DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)  
可扩展交换机扩展将调用此函数以减少端口的引用计数器。

如果扩展将调用[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)，它必须调用[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)后[OID\_交换机\_NIC\_请求](https://msdn.microsoft.com/library/windows/hardware/hh598266)或[ **NDIS\_状态\_交换机\_NIC\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598205)指示已完成。

 

 





