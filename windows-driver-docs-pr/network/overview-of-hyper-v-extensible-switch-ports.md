---
title: Hyper-V 可扩展交换机端口概述
description: Hyper-V 可扩展交换机端口概述
ms.assetid: FD6B6014-B840-4EC8-96F4-34C08EC303EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09bc9a53e2b1df378b524a17daedd232d0de279
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843741"
---
# <a name="overview-of-hyper-v-extensible-switch-ports"></a>Hyper-V 可扩展交换机端口概述


到 Hyper-v 可扩展交换机的每个网络连接都由端口表示。 可扩展交换机接口在建立网络连接之前创建和配置端口。 网络连接断开后，接口可能会删除该端口或将其重新用于其他网络连接。

使用网络接口配置的每个 Hyper-v 子分区在可扩展交换机上都分配有一个端口。 启动 Hyper-v 子分区时，可扩展交换机接口会在来宾操作系统内公开虚拟机（VM）网络适配器之前创建端口。 公开并初始化 VM 网络适配器后，可扩展交换机接口会在 VM 网络适配器和可扩展交换机端口之间创建网络连接。 如果子分区已停止，可扩展交换机接口首先会删除网络连接，然后删除可扩展交换机端口。

创建可扩展交换机端口时，会使用唯一标识符和名称对其进行配置。 创建可扩展交换机端口后，可将其设置为策略，这些策略定义用于通过端口管理数据包流量的各种属性。 例如，可以为虚拟 LAN （VLAN）属性和端口流量的访问限制定义标准端口策略。 此外，独立的软件供应商（Isv）可以定义单独端口可以设置的自定义策略。 有关详细信息，请参阅[端口策略](port-policies.md)。

可扩展的交换机端口包含以下类型：

<a href="" id="validation-ports"></a>验证端口  
验证端口用于验证和验证端口设置。 这些端口是临时的，在某些情况下会创建。

例如，当创建或重新配置 Hyper-v 子分区以进行网络访问时，可扩展交换机接口会创建一个验证端口。 接口使用此端口验证与分区的虚拟机（VM）网络适配器的网络连接的设置。 验证完成后，将删除验证端口，并创建一个操作端口。

有关详细信息，请参阅[验证端口](validation-ports.md)。

<a href="" id="operational-ports"></a>操作端口  
创建操作端口以托管可扩展交换机网络适配器连接。 创建操作端口后，将为其分配端口类型。 此端口类型在创建端口之后和被破坏之前有效。 对于分配给 Hyper-v 子分区的端口，操作端口类型在分区运行和运行时保持有效。

有关详细信息，请参阅[操作端口](operational-ports.md)。

可扩展交换机扩展通过以下可扩展交换机对象标识符（OID）请求通知端口创建、更新和删除操作：

<a href="" id="oid-switch-port-create"></a>[OID\_交换机\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)  
可扩展交换机的协议边缘发出 oid [\_switch\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)的 oid 集请求，\_CREATE 来通知可扩展交换机扩展有关创建可扩展交换机端口的信息。

扩展可以通过返回\_数据\_不\_为 OID 请求接受的状态来否决创建通知。 例如，如果扩展无法分配资源来强制在端口上配置策略，则扩展 vetoes 创建通知。

如果扩展插件接受创建通知，则必须在可扩展交换机驱动程序堆栈中向下转发 OID 请求。 扩展会监视此 OID 请求的完成状态，以确定基础扩展是否否决了端口创建通知。

在创建网络连接之前，扩展不能将数据包转发到新创建的端口。 有关此过程的详细信息，请参阅[Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

<a href="" id="oid-switch-port-updated"></a>[OID\_交换机\_端口\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)  
可扩展交换机的协议边缘发出 oid [\_switch\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)的 oid 集请求\_更新，通知可扩展交换机端口的参数正在更新。 仅对已创建且尚未开始拆卸/删除进程的端口发出 OID。 目前只能在创建后更新*PortFriendlyName*字段。

当之前到端口的网络连接已断开并且端口的所有 OID 请求均已完成时，可扩展交换机的协议边缘会发出此 OID 请求。

**请注意**  如果之前未对端口进行网络适配器连接，则可能发出此 OID 请求。

 

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

<a href="" id="oid-switch-port-teardown"></a>[OID\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)  
可扩展交换机的协议边缘[\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)发出 oid 集请求，以通知可扩展交换机扩展正在删除的可扩展交换机端口。 当之前到端口的网络连接已断开并且端口的所有 OID 请求均已完成时，可扩展交换机的协议边缘会发出此 OID 请求。

**请注意**  如果之前未对端口进行网络适配器连接，则可能发出此 OID 请求。

 

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

扩展转发此 OID 请求后，它将无法再为删除的端口发出 OID 请求。

<a href="" id="oid-switch-port-delete"></a>[OID\_交换机\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)  
可扩展交换机的协议边缘[\_交换机\_端口\_"删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)" 发出 oid 集请求，以通知可扩展交换机扩展已删除可扩展交换机端口。 可扩展交换机的协议边缘在发出 Oid 后发出此 OID 请求[\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)请求，以及针对该端口的 OID 请求已完成。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

为网络连接创建的所有可扩展交换机端口都被分配一个大于 NDIS 的标识符 **\_交换机\_默认\_端口\_ID**。 **NDIS\_交换机\_默认\_端口\_ID**标识符保留并按以下方式使用：

-   数据包的源端口标识符存储在数据包的带外（OOB）转发上下文中，该上下文与其[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构关联。 NDIS\_交换机的源端口标识符 **\_默认\_端口\_ID**指定数据包源自可扩展交换机扩展，而不是来自可扩展交换机端口。 具有 NDIS\_交换机的源端口标识符的数据包 **\_默认\_端口\_ID**是受信任的，并且会绕过可扩展交换机端口策略，如访问控制列表（acl）和服务质量（QoS）。

    扩展可能需要将数据包视为来自特定端口。 这允许将该端口的策略应用到该数据包。 该扩展调用[*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)来更改数据包的源端口。

    但在某些情况下，扩展可能需要将数据包的源端口标识符分配给**NDIS\_交换机\_默认\_端口\_ID**。 例如，扩展可能需要将源端口标识符设置为**NDIS\_交换机\_默认\_端口\_ID**发送到外部网络上的设备的专用控制数据包。

    有关转发上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   OID\_交换机的对象标识符（OID）请求[\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)由可扩展交换机接口发出，以封装颁发给可扩展交换机外部网络适配器的 oid 请求。 例如，在通过可扩展交换机驱动程序堆栈向下发出硬件卸载 OID 请求之前，这些请求将由接口封装。

    扩展还可以发出封装的 OID 请求，以便向下转发请求的可扩展交换机控制路径。 这允许扩展插件查询或配置基础物理网络适配器的功能。

    此 OID 请求 **\_请求结构的 ndis\_OID**的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的指针。 如果**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**，这将指定 OID 请求是由可扩展交换机接口发出的。 如果将**DestinationPortId**设置为**NDIS\_交换机\_默认\_端口\_ID**，则指定 OID 请求将由可扩展交换机驱动程序堆栈中的扩展进行处理。

    有关 OID 请求的控制路径的详细信息，请参阅[Oid 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

-   Ndis 状态指示， [**ndis\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)由可扩展交换机的微型端口边缘颁发，以封装可扩展交换机外部网络适配器的状态指示。

    扩展还可以发出封装的 NDIS 状态指示，以便向前指示可扩展交换机控制路径。 这允许扩展更改基础物理网络适配器的已报告功能。

    对于此指示， [**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的指针。 如果**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**，则指定状态指示是由可扩展交换机接口发出的。 如果将**DestinationPortId**设置为**NDIS\_交换机\_默认\_端口\_ID**，则指定 OID 请求将由可扩展交换机驱动程序堆栈中的扩展进行处理。

    有关 NDIS 状态指示的控制路径的详细信息，请参阅[适用于 Ndis 状态指示的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-ndis-status-indications.md)。

可扩展交换机接口为已创建的每个端口维护一个引用计数器。 如果端口引用计数器的值为非零值，则不会删除该端口。 接口提供以下处理程序函数来递增或递减可扩展交换机端口的引用计数器：

<a href="" id="referenceswitchport"></a>[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展调用此函数来递增端口的引用计数器。 虽然引用计数器具有非零值，但可扩展交换机的协议边缘不会发出[OID\_switch\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)的对象标识符（OID）设置请求，\_delete 删除可扩展交换机端口。

扩展必须在执行任何需要端口处于活动状态的操作之前调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 。 例如，扩展必须先调用*ReferenceSwitchPort* ，然后才能发出[oid\_SWITCH\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)中的 oid 方法请求。

**请注意**  扩展在收到 OID 的 oid 集请求后不得为该端口调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) [\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)该端口。

 

<a href="" id="dereferenceswitchport"></a>[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展调用此函数来减小端口的引用计数器。

在对端口执行的操作完成后，扩展必须调用[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 。 例如，如果在[\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)请求之前，调用*ReferenceSwitchPort*\_之前调用了该扩展，则扩展必须在 OID 请求后调用*DereferenceSwitchPort*完成.

**请注意**  NDIS 端口和可扩展交换机端口都是不同的对象。 在可扩展交换机数据路径间移动的数据包始终分配给 ndis 端口号， **\_默认\_端口\_号**。 但是，数据包的源和目标可扩展交换机端口号可以是**NDIS\_交换机\_默认\_端口\_ID**或更高版本的值。 有关详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

 





