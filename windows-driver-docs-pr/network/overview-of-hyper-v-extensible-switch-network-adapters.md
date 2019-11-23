---
title: Hyper-V 可扩展交换机网络适配器概述
description: Hyper-V 可扩展交换机网络适配器概述
ms.assetid: 61403FDE-90BF-4D0A-83E1-5AF8ADBD37A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab83f981cbcbaea6e437d848d7eeca96613cf2ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843746"
---
# <a name="overview-of-hyper-v-extensible-switch-network-adapters"></a>Hyper-V 可扩展交换机网络适配器概述


Hyper-v 可扩展交换机支持来自各种类型的虚拟或物理网络适配器的连接。 通过可扩展交换机端口建立与这些类型的网络适配器的连接。 端口是在建立虚拟网络适配器之前创建的，并且在网络适配器连接断开后被删除。

例如，当启动 Hyper-v 子分区时，可扩展交换机接口会在来宾操作系统内公开虚拟机（VM）网络适配器之前创建端口。 公开并枚举 VM 网络适配器后，可扩展交换机接口会在 VM 网络适配器和可扩展交换机端口之间创建网络连接。 如果子分区已停止，可扩展交换机接口首先会删除网络连接，然后删除可扩展交换机端口。

Hyper-v 可扩展交换机支持以下类型的虚拟网络适配器的连接：

<a href="" id="external-network-adapters"></a>外部网络适配器  
这是在 Hyper-v 父分区中运行的管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机仅支持一个外部网络适配器连接。

外部网络适配器提供主机上的物理网络接口的连接。 Hyper-v 父分区和所有子分区都可以访问外部网络适配器。

有关此类网络适配器的详细信息，请参阅[外部网络适配器](external-network-adapters.md)。

<a href="" id="internal-network-adapters"></a>内部网络适配器  
这是在 Hyper-v 父分区中运行的管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机只支持一个内部网络适配器连接。

内部网络适配器提供对在管理操作系统中运行的进程的可扩展交换机的访问。 这允许这些进程通过可扩展交换机发送或接收数据包。

有关此类网络适配器的详细信息，请参阅[内部网络适配器](internal-network-adapters.md)。

<a href="" id="virtual-machine--vm--network-adapters"></a>虚拟机（VM）网络适配器  
这是在来宾操作系统中公开的可扩展交换机网络适配器，该适配器在 Hyper-v 子分区中运行。

**请注意**，hyper-v 中的  ，子分区也称为 VM。

 

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可以是网络适配器（*合成网络适配器*）的综合虚拟化。 在这种情况下，VM 中运行的网络虚拟服务客户端（Netvsc.sys）将公开此虚拟网络适配器。 Netvsc.sys 通过 VM 总线（VMBus）将数据包转发到可扩展交换机端口并从该端口转发。

-   VM 网络适配器可以是物理网络适配器的模拟虚拟化（*仿真网络适配器*）。 在这种情况下，VM 网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到可扩展交换机端口并将其从可扩展交换机端口转发。

有关此类网络适配器的详细信息，请参阅[虚拟机网络适配器](virtual-machine-network-adapters.md)。

可扩展交换机网络适配器连接通过以下可扩展交换机 OID 请求来创建、更新和删除：

<a href="" id="oid-switch-nic-create"></a>[OID\_交换机\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)  
可扩展交换机的协议边缘发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)的 oid 集请求，\_创建通知可扩展交换机扩展与创建与可扩展交换机端口的网络适配器连接有关。 端口之前必须已通过 oid [\_SWITCH\_端口\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)创建。

[OID\_交换机\_NIC\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)请求仅通知扩展：正在启动新的可扩展交换机网络适配器连接，并且包流量很快就会通过指定端口开始发生。

扩展可以通过返回\_数据\_不\_为 OID 请求接受的状态来否决创建通知。 例如，如果某个扩展无法满足用于网络适配器连接的端口上的配置策略，则该扩展应否决创建通知。

如果扩展插件接受创建通知，则必须在可扩展交换机驱动程序堆栈中向下转发 OID 请求。 扩展会监视此 OID 请求的完成状态，以确定基础扩展是否否决了创建通知。

创建网络适配器连接后，将为其分配一个 NDIS\_交换机\_NIC\_索引值。 此索引值标识可扩展交换机端口上的网络适配器连接。 已为到外部、内部和 VM 网络适配器的连接分配了 NDIS\_交换机\_NIC\_索引 **\_\_** 值。\_\_ 绑定到外部网络适配器的每个物理或虚拟网络适配器都按以下方式分配了 NDIS\_交换机\_NIC\_索引值：

-   如果物理网络适配器或虚拟网络适配器直接绑定到外部网络适配器，则会为其分配一个 NDIS\_交换机\_NIC\_索引值为1。

-   如果物理网络适配器是可扩展交换机组的一部分，则会为其分配一个 NDIS\_交换机\_NIC\_索引值大于或等于1。 可扩展的交换机团队是一种配置，其中一个或多个物理网络适配器的团队绑定到可扩展交换机外部网络适配器。

有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

有关 NDIS\_交换机\_NIC\_索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

**请注意**  扩展无法通过网络适配器连接生成或转发数据包，直到可扩展交换机的协议边缘发出 OID 的 oid 集请求[\_交换机\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)。

 

<a href="" id="oid-switch-nic-connect"></a>[OID\_交换机\_NIC\_连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)  
可扩展交换机的协议边缘发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)的 oid 集请求\_"连接"，以通知可扩展交换机网络适配器连接是否完全正常运行。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

完成 OID 请求并将 NDIS\_状态\_成功后，网络适配器连接和可扩展交换机端口都可完全正常运行。 当网络适配器连接处于此状态时，扩展可以执行以下操作：

-   生成或转发到端口的网络适配器连接的数据包流量。

-   颁发可扩展交换机 Oid，或使用端口作为源端口的状态指示。

-   调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)为网络适配器连接递增引用计数器。 当引用计数器的值为非零值时，可扩展交换机接口将不会断开网络适配器连接。

<a href="" id="oid-switch-nic-updated"></a>[OID\_交换机\_NIC\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-updated)  
可扩展交换机的协议边缘发出 oid\_SWITCH\_NIC 的 OID 集请求\_已更新，以通知可扩展交换机网络适配器的参数已更新的可扩展交换机扩展。 仅为已连接并且尚未开始断开连接过程的 Nic 发出 OID。 这些运行时配置更改可以包括*NicFriendlyName*、 *MTU*、 *NetCfgInstanceId*、 *PermanentMacAddress*、 *VMMacAddress*、 *CurrentMacAddress*和*VFAssigned。*

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

<a href="" id="oid-switch-nic-disconnect"></a>[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)  
可扩展交换机的协议边缘发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)的 oid 集请求\_"断开连接"，通知可扩展交换机网络适配器连接正在被破坏的可扩展交换机扩展。 完全断开连接后，可扩展交换机的协议边缘会发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)的 oid 集请求\_删除。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

扩展转发此 OID 请求后，不能再生成数据包或将数据包转发到网络适配器连接被断开的端口。 此外，此扩展不能再为网络适配器连接调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 。

<a href="" id="oid-switch-nic-delete"></a>[OID\_交换机\_NIC\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)  
可扩展交换机的协议边缘发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)的 oid 集请求\_"删除"，以通知可扩展交换机网络适配器连接已断开并被删除。 此 OID 请求仅针对以下网络连接发出： oid 设置的 oid [\_开关\_NIC\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)之前发出断开。

**请注意**  扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

 

完成此 OID 请求之后，可扩展交换机的协议边缘会发出 oid [\_switch\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)请求，以启动用于网络适配器连接的端口的删除过程。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

可扩展交换机接口为已创建的每个网络适配器连接维护一个引用计数器。 如果网络适配器的引用计数器具有非零值，则不会将其删除。 接口提供以下处理程序函数来递增或递减可扩展交换机网络适配器连接的引用计数器：

<a href="" id="referenceswitchnic"></a>[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)  
可扩展交换机扩展调用此函数以增加网络适配器连接的引用计数器。 虽然引用计数器具有非零值，但可扩展交换机接口不会删除网络适配器连接。

扩展应在执行以下操作之前调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ：

-   将[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)请求按下扩展到底层的外部适配器。

-   将[**NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)状态指示从底层外部适配器的可扩展交换机驱动程序堆栈。

**请注意**  扩展在收到\_OID 的 oid 集请求后，不能为网络适配器连接调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) [\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)连接。

 

<a href="" id="dereferenceswitchnic"></a>[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)  
可扩展交换机扩展调用此函数来减小端口的引用计数器。

如果扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)，则它必须在 OID 后调用[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) [\_交换机\_nic\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)或[**NDIS\_状态\_交换机\_nic\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示已完成。

 

 





