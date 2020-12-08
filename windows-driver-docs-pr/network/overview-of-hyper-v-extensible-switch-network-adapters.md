---
title: Hyper-V 可扩展交换机网络适配器概述
description: Hyper-V 可扩展交换机网络适配器概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78b26412f50ac4ae7341404f2152ac1aaf99e8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829205"
---
# <a name="overview-of-hyper-v-extensible-switch-network-adapters"></a>Hyper-V 可扩展交换机网络适配器概述


Hyper-v 可扩展交换机支持来自各种类型的虚拟或物理网络适配器的连接。 通过可扩展交换机端口建立与这些类型的网络适配器的连接。 端口是在建立虚拟网络适配器之前创建的，并且在网络适配器连接断开后被删除。

例如，启动 Hyper-v 子分区时，可扩展交换机接口会在虚拟机 (VM) 网络适配器在来宾操作系统内公开之前创建端口。 公开并枚举 VM 网络适配器后，可扩展交换机接口会在 VM 网络适配器和可扩展交换机端口之间创建网络连接。 如果子分区已停止，可扩展交换机接口首先会删除网络连接，然后删除可扩展交换机端口。

Hyper-v 可扩展交换机支持以下类型的虚拟网络适配器的连接：

<a href="" id="external-network-adapters"></a>外部网络适配器  
这是在 Hyper-v 父分区中运行的管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机仅支持一个外部网络适配器连接。

外部网络适配器提供主机上的物理网络接口的连接。 Hyper-v 父分区和所有子分区都可以访问外部网络适配器。

有关此类网络适配器的详细信息，请参阅 [外部网络适配器](external-network-adapters.md)。

<a href="" id="internal-network-adapters"></a>内部网络适配器  
这是在 Hyper-v 父分区中运行的管理操作系统中公开的可扩展交换机网络适配器。 每个可扩展交换机只支持一个内部网络适配器连接。

内部网络适配器提供对在管理操作系统中运行的进程的可扩展交换机的访问。 这允许这些进程通过可扩展交换机发送或接收数据包。

有关此类网络适配器的详细信息，请参阅 [内部网络适配器](internal-network-adapters.md)。

<a href="" id="virtual-machine--vm--network-adapters"></a>虚拟机 (VM) 网络适配器  
这是在来宾操作系统中公开的可扩展交换机网络适配器，该适配器在 Hyper-v 子分区中运行。

**注意**  在 Hyper-v 中，子分区也称为 VM。

 

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可以是网络适配器 (合成 *网络* 适配器) 的综合虚拟化。 在这种情况下，VM 中运行的网络虚拟服务客户端 (Netvsc.sys) 将公开此虚拟网络适配器。 Netvsc.sys)  (VMBus，将数据包转发到可扩展交换机端口，并将其从可扩展交换机端口转发。

-   VM 网络适配器可以是物理网络适配器的模拟虚拟化 (*仿真网络适配器*) 。 在这种情况下，VM 网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到可扩展交换机端口并将其从可扩展交换机端口转发。

有关此类网络适配器的详细信息，请参阅 [虚拟机网络适配器](virtual-machine-network-adapters.md)。

可扩展交换机网络适配器连接通过以下可扩展交换机 OID 请求来创建、更新和删除：

<a href="" id="oid-switch-nic-create"></a>[OID \_ 交换机 \_ NIC \_ 创建](./oid-switch-nic-create.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md) 的 oid 集请求，通知与创建可扩展交换机端口的网络适配器连接有关的可扩展交换机扩展。 之前必须通过 oid [ \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md)的 oid 集请求创建端口。

[OID \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md)请求仅通知扩展：正在启动新的可扩展交换机网络适配器连接，并且包流量很快就会在指定的端口上发生。

此扩展可以通过返回 \_ \_ OID 请求的 "不接受" 状态数据来否决创建通知 \_ 。 例如，如果某个扩展无法满足用于网络适配器连接的端口上的配置策略，则该扩展应否决创建通知。

如果扩展插件接受创建通知，则必须在可扩展交换机驱动程序堆栈中向下转发 OID 请求。 扩展会监视此 OID 请求的完成状态，以确定基础扩展是否否决了创建通知。

当创建网络适配器连接时，将为其分配 NDIS \_ 交换机 \_ NIC \_ 索引值。 此索引值标识可扩展交换机端口上的网络适配器连接。 与外部、内部和 VM 网络适配器的连接为 \_ \_ \_ **ndis \_ 交换机 \_ 默认 \_ nic \_ 索引** 分配了 ndis 交换机 NIC 索引值。 每个绑定到外部网络适配器的物理网络适配器或虚拟网络适配器都 \_ 按以下方式分配了 NDIS 交换机 \_ NIC \_ 索引值：

-   如果物理网络适配器或虚拟网络适配器直接绑定到外部网络适配器，则会将该适配器的 NDIS \_ 交换机 \_ NIC 索引值指定为 \_ 1。

-   如果物理网络适配器是可扩展交换机组的一部分，则会为其分配一个 \_ \_ \_ 大于或等于1的 NDIS 交换机 NIC 索引值。 可扩展的交换机团队是一种配置，其中一个或多个物理网络适配器的团队绑定到可扩展交换机外部网络适配器。

有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

有关 NDIS \_ 交换机 \_ NIC 索引值的详细信息 \_ ，请参阅 [网络适配器索引值](network-adapter-index-values.md)。

**注意**  扩展无法通过网络适配器连接生成或转发数据包，直到可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md)的 oid 集请求。

 

<a href="" id="oid-switch-nic-connect"></a>[OID \_ 交换机 \_ NIC \_ 连接](./oid-switch-nic-connect.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md) 的 oid 集请求，以通知可扩展交换机网络适配器连接完全正常运行。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

完成 OID 请求 \_ \_ 并成功完成后，网络适配器连接和可扩展交换机端口将完全正常运行。 当网络适配器连接处于此状态时，扩展可以执行以下操作：

-   生成或转发到端口的网络适配器连接的数据包流量。

-   颁发可扩展交换机 Oid，或使用端口作为源端口的状态指示。

-   调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 为网络适配器连接递增引用计数器。 当引用计数器的值为非零值时，可扩展交换机接口将不会断开网络适配器连接。

<a href="" id="oid-switch-nic-updated"></a>[\_ \_ 已更新 OID 交换机 NIC \_](./oid-switch-nic-updated.md)  
可扩展交换机的协议边缘发出 oid 交换机 NIC 更新的 OID 集请求 \_ \_ \_ ，以通知可扩展交换机网络适配器的参数已更新的可扩展交换机扩展。 仅为已连接并且尚未开始断开连接过程的 Nic 发出 OID。 这些运行时配置更改可以包括 *NicFriendlyName*、 *MTU*、 *NetCfgInstanceId*、 *PermanentMacAddress*、 *VMMacAddress*、 *CurrentMacAddress* 和 *VFAssigned。*

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

<a href="" id="oid-switch-nic-disconnect"></a>[OID \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md) 的 oid 集请求，以通知可扩展交换机网络适配器连接正在被切断的可扩展交换机扩展。 完全断开连接后，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ DELETE](./oid-switch-nic-delete.md)的 oid 设置请求。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

扩展转发此 OID 请求后，不能再生成数据包或将数据包转发到网络适配器连接被断开的端口。 此外，此扩展不能再为网络适配器连接调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 。

<a href="" id="oid-switch-nic-delete"></a>[OID \_ 交换机 \_ NIC \_ 删除](./oid-switch-nic-delete.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ DELETE](./oid-switch-nic-delete.md) 的 oid 集请求，以通知可扩展交换机网络适配器连接已断开并被删除。 此 OID 请求仅针对网络连接发出，该网络连接之前已发出 oid [ \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md) 的 oid 设置请求。

**注意**  扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

 

完成此 OID 请求后，可扩展交换机的协议边缘将发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md) 的 oid 设置请求，以启动用于网络适配器连接的端口的删除过程。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

可扩展交换机接口为已创建的每个网络适配器连接维护一个引用计数器。 如果网络适配器的引用计数器具有非零值，则不会将其删除。 接口提供以下处理程序函数来递增或递减可扩展交换机网络适配器连接的引用计数器：

<a href="" id="referenceswitchnic"></a>[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)  
可扩展交换机扩展调用此函数以增加网络适配器连接的引用计数器。 虽然引用计数器具有非零值，但可扩展交换机接口不会删除网络适配器连接。

扩展应在执行以下操作之前调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ：

-   将 [OID \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) 请求按下了可扩展交换机驱动程序堆栈。

-   将 [**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 状态指示从底层的外部适配器中进行可扩展交换机驱动程序堆栈。

**注意** 此扩展在收到对该连接的 [oid \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md)的 oid 集请求后不得为网络适配器连接调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 。

 

<a href="" id="dereferenceswitchnic"></a>[*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)  
可扩展交换机扩展调用此函数来减小端口的引用计数器。

如果扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)，则它必须在 [OID \_ 交换机 \_ nic \_ 请求](./oid-switch-nic-request.md)或 [**NDIS \_ 状态 \_ 切换 \_ nic \_ 状态**](./ndis-status-switch-nic-status.md)指示完成后调用 [*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) 。

 

