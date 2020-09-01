---
title: Hyper-V 可扩展交换机端口概述
description: Hyper-V 可扩展交换机端口概述
ms.assetid: FD6B6014-B840-4EC8-96F4-34C08EC303EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0384a784b24785ff33a124c2d292c2ccc5cc362d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206293"
---
# <a name="overview-of-hyper-v-extensible-switch-ports"></a>Hyper-V 可扩展交换机端口概述


到 Hyper-v 可扩展交换机的每个网络连接都由端口表示。 可扩展交换机接口在建立网络连接之前创建和配置端口。 网络连接断开后，接口可能会删除该端口或将其重新用于其他网络连接。

使用网络接口配置的每个 Hyper-v 子分区在可扩展交换机上都分配有一个端口。 启动 Hyper-v 子分区时，可扩展交换机接口会在虚拟机 (VM) 网络适配器在来宾操作系统内公开之前创建端口。 公开并初始化 VM 网络适配器后，可扩展交换机接口会在 VM 网络适配器和可扩展交换机端口之间创建网络连接。 如果子分区已停止，可扩展交换机接口首先会删除网络连接，然后删除可扩展交换机端口。

创建可扩展交换机端口时，会使用唯一标识符和名称对其进行配置。 创建可扩展交换机端口后，可将其设置为策略，这些策略定义用于通过端口管理数据包流量的各种属性。 例如，可以为虚拟 LAN 定义标准端口策略 (VLAN) 属性和端口流量的访问限制。 此外，独立的软件供应商 (Isv) 可以定义单独端口可用于设置的自定义策略。 有关详细信息，请参阅 [端口策略](port-policies.md)。

可扩展的交换机端口包含以下类型：

<a href="" id="validation-ports"></a>验证端口  
验证端口用于验证和验证端口设置。 这些端口是临时的，在某些情况下会创建。

例如，当创建或重新配置 Hyper-v 子分区以进行网络访问时，可扩展交换机接口会创建一个验证端口。 接口使用此端口验证与分区 (VM) 网络适配器的网络连接的设置。 验证完成后，将删除验证端口，并创建一个操作端口。

有关详细信息，请参阅 [验证端口](validation-ports.md)。

<a href="" id="operational-ports"></a>操作端口  
创建操作端口以托管可扩展交换机网络适配器连接。 创建操作端口后，将为其分配端口类型。 此端口类型在创建端口之后和被破坏之前有效。 对于分配给 Hyper-v 子分区的端口，操作端口类型在分区运行和运行时保持有效。

有关详细信息，请参阅 [操作端口](operational-ports.md)。

可通过以下可扩展交换机对象标识符 (OID) 请求，通知可扩展交换机扩展：

<a href="" id="oid-switch-port-create"></a>[OID \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md) 的 oid 集请求，通知有关创建可扩展交换机端口的可扩展交换机扩展。

此扩展可以通过返回 \_ \_ OID 请求的 "不接受" 状态数据来否决创建通知 \_ 。 例如，如果扩展无法分配资源来强制在端口上配置策略，则扩展 vetoes 创建通知。

如果扩展插件接受创建通知，则必须在可扩展交换机驱动程序堆栈中向下转发 OID 请求。 扩展会监视此 OID 请求的完成状态，以确定基础扩展是否否决了端口创建通知。

在创建网络连接之前，扩展不能将数据包转发到新创建的端口。 有关此过程的详细信息，请参阅 [Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

<a href="" id="oid-switch-port-updated"></a>[\_ \_ 已更新 OID 交换机端口 \_](./oid-switch-port-updated.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 更新](./oid-switch-port-updated.md) 的 oid 设置请求，以通知可扩展交换机端口的参数正在更新。 仅对已创建且尚未开始拆卸/删除进程的端口发出 OID。 目前只能在创建后更新 *PortFriendlyName* 字段。

当之前到端口的网络连接已断开并且端口的所有 OID 请求均已完成时，可扩展交换机的协议边缘会发出此 OID 请求。

**注意**   如果之前未对端口进行网络适配器连接，则可能发出此 OID 请求。

 

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

<a href="" id="oid-switch-port-teardown"></a>[OID \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md) 请求，以通知可扩展交换机扩展正在删除的可扩展交换机端口。 当之前到端口的网络连接已断开并且端口的所有 OID 请求均已完成时，可扩展交换机的协议边缘会发出此 OID 请求。

**注意**   如果之前未对端口进行网络适配器连接，则可能发出此 OID 请求。

 

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

扩展转发此 OID 请求后，它将无法再为删除的端口发出 OID 请求。

<a href="" id="oid-switch-port-delete"></a>[\_删除 OID 交换机 \_ 端口 \_](./oid-switch-port-delete.md)  
可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ DELETE](./oid-switch-port-delete.md) 的 oid 集请求，以通知可扩展交换机扩展已删除可扩展交换机端口。 可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md) 请求后发出此 oid 请求，并已完成针对该端口的 oid 请求。

扩展必须始终按可扩展交换机驱动程序堆栈转发此 OID 设置请求。 此扩展不能导致请求失败。

为网络连接创建的所有可扩展交换机端口都被分配一个大于 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**的标识符。 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**标识符被保留，并按以下方式使用：

-   数据包的源端口标识符存储在数据包的带外 (OOB) 转发上下文与其 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构关联。 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**的源端口标识符指定数据包源自可扩展交换机扩展，而不是来自可扩展交换机端口。 具有 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 的源端口标识符的数据包是受信任的，并且绕过可扩展交换机端口策略，如访问控制列表 (Acl) 和服务质量 (QoS) 。

    扩展可能需要将数据包视为来自特定端口。 这允许将该端口的策略应用到该数据包。 该扩展调用 [*SetNetBufferListSource*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source) 来更改数据包的源端口。

    但在某些情况下，扩展可能需要将数据包的源端口标识符分配给 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。 例如，对于发送到外部网络上的设备的专有控制数据包，扩展可能需要将源端口标识符设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 。

    有关转发上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   对象标识符 (oid [ \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md)) 请求由可扩展交换机接口发出，以封装颁发给可扩展交换机外部网络适配器的 oid 请求。 例如，在通过可扩展交换机驱动程序堆栈向下发出硬件卸载 OID 请求之前，这些请求将由接口封装。

    扩展还可以发出封装的 OID 请求，以便向下转发请求的可扩展交换机控制路径。 这允许扩展插件查询或配置基础物理网络适配器的功能。

    此 OID 请求的**ndis \_ OID \_ 请求**结构的**InformationBuffer**成员包含指向[**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的指针。 如果将 **SourcePortId** 成员设置为 **NDIS \_ 切换 \_ 默认 \_ 端口 \_ ID**，则这将指定 OID 请求是由可扩展交换机接口发出的。 如果将 " **DestinationPortId** " 设置为 " **NDIS \_ 切换 \_ 默认 \_ 端口 \_ ID**"，则此选项指定 OID 请求将由可扩展交换机驱动程序堆栈中的扩展进行处理。

    有关 OID 请求的控制路径的详细信息，请参阅 [Oid 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

-   [**Ndis \_ 状态 \_ 交换机 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md)的 ndis 状态指示由可扩展交换机的微型端口边缘颁发，以封装可扩展交换机外部网络适配器的状态指示。

    扩展还可以发出封装的 NDIS 状态指示，以便向前指示可扩展交换机控制路径。 这允许扩展更改基础物理网络适配器的已报告功能。

    此指示的[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**NDIS \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的指针。 如果将 **SourcePortId** 成员设置为 **NDIS \_ 切换 \_ 默认 \_ 端口 \_ ID**，这将指定状态指示是由可扩展交换机接口发出的。 如果将 " **DestinationPortId** " 设置为 " **NDIS \_ 切换 \_ 默认 \_ 端口 \_ ID**"，则此选项指定 OID 请求将由可扩展交换机驱动程序堆栈中的扩展进行处理。

    有关 NDIS 状态指示的控制路径的详细信息，请参阅 [适用于 Ndis 状态指示的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-ndis-status-indications.md)。

可扩展交换机接口为已创建的每个端口维护一个引用计数器。 如果端口引用计数器的值为非零值，则不会删除该端口。 接口提供以下处理程序函数来递增或递减可扩展交换机端口的引用计数器：

<a href="" id="referenceswitchport"></a>[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展调用此函数来递增端口的引用计数器。 虽然引用计数器的值为非零值，但可扩展交换机的协议边缘不会 (OID 发出对象标识符) 设置 [oid \_ 交换机 \_ 端口 \_ delete](./oid-switch-port-delete.md) 的请求来删除可扩展交换机端口。

扩展必须在执行任何需要端口处于活动状态的操作之前调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 。 例如，扩展必须先调用 *ReferenceSwitchPort* ，然后才会发出 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](./oid-switch-port-property-enum.md)的 oid 方法请求。

**注意**   当某个端口收到 oid 设置的 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md)请求时，它不能为该端口调用[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 。

 

<a href="" id="dereferenceswitchport"></a>[*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展调用此函数来减小端口的引用计数器。

在对端口执行的操作完成后，扩展必须调用 [*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 。 例如，如果在发出[oid \_ 交换 \_ 端口 \_ 属性 \_ 枚举](./oid-switch-port-property-enum.md)请求之前调用了*ReferenceSwitchPort*的扩展，则扩展必须在完成 oid 请求后调用*DereferenceSwitchPort* 。

**注意**   NDIS 端口和可扩展交换机端口都是不同的对象。 在可扩展交换机数据路径间移动的数据包始终分配给 ndis 端口号 **ndis \_ 默认 \_ 端口 \_ 号**。 但是，数据包的源和目标可扩展交换机端口号可以是 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID** 或更高的值。 有关详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

