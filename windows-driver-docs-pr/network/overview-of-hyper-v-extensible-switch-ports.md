---
title: Hyper-V 可扩展交换机端口概述
description: Hyper-V 可扩展交换机端口概述
ms.assetid: FD6B6014-B840-4EC8-96F4-34C08EC303EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ff01d32f99f523035d60dad4cf15d3e7ed6d818
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385719"
---
# <a name="overview-of-hyper-v-extensible-switch-ports"></a>Hyper-V 可扩展交换机端口概述


每个网络连接到 HYPER-V 可扩展交换机是由端口表示。 可扩展交换机接口创建并配置一个端口，才能建立网络连接。 网络连接，则将调用后，接口可能会删除该端口或它重用于另一个网络连接。

与网络接口配置每个 HYPER-V 子分区分配可扩展交换机上的端口。 启动 HYPER-V 子分区时，可扩展交换机接口之前在来宾操作系统中公开的虚拟机 (VM) 网络适配器创建一个端口。 公开 VM 网络适配器并将其初始化后，可扩展交换机接口用于创建 VM 网络适配器和可扩展的交换机端口之间的网络连接。 如果子分区已停止，可扩展交换机接口删除网络连接，，然后删除可扩展交换机端口。

创建可扩展交换机端口时，它被配置的唯一标识符和名称。 创建后，可扩展交换机端口可预配通过端口定义的数据包流量管理的各种属性的策略。 例如，标准端口策略可以定义的虚拟 LAN (VLAN) 属性和端口的流量的访问限制。 此外，独立软件供应商 (Isv) 可以定义可预配单个端口的自定义策略。 有关详细信息，请参阅[端口策略](port-policies.md)。

可扩展的交换机端口包括以下类型：

<a href="" id="validation-ports"></a>验证端口  
验证端口用于验证和验证端口设置。 这些端口是临时的在某些情况下创建。

例如，当创建或重新配置为使用网络访问权限的 HYPER-V 子分区时，可扩展交换机接口创建验证端口。 接口使用此端口来验证该分区的网络连接到虚拟机 (VM) 网络适配器的设置。 完成验证后，删除验证端口和创建操作的端口。

有关详细信息，请参阅[验证端口](validation-ports.md)。

<a href="" id="operational-ports"></a>操作端口  
创建操作端口来承载不可扩展交换机的网络适配器连接。 创建操作的端口时，它被分配端口类型。 创建端口后，在它，则将调用之前，此端口类型将生效。 为端口分配给 HYPER-V 子分区，分区时运行和操作的操作的端口类型一直有效。

有关详细信息，请参阅[操作端口](operational-ports.md)。

可扩展的交换机扩展会通知你端口创建、 更新和删除通过以下可扩展交换机对象标识符 (OID) 请求：

<a href="" id="oid-switch-port-create"></a>[OID\_交换机\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)以通知有关的可扩展交换机端口创建可扩展的交换机扩展。

该扩展可以通过返回状态来禁止创建通知\_数据\_不\_OID 请求被接受。 例如，如果扩展不能分配资源，以强制实施其配置的端口上的策略，该扩展 vetoes 创建通知。

如果扩展接受创建通知，它必须转发 OID 请求下可扩展交换机驱动程序堆栈。 扩展监视此 OID 请求以确定基础扩展是否已被否决端口创建通知的完成状态。

扩展不能将数据包转发到新创建的端口之前创建的网络连接。 此过程的详细信息，请参阅[HYPER-V 可扩展交换机的网络适配器](hyper-v-extensible-switch-network-adapters.md)。

<a href="" id="oid-switch-port-updated"></a>[OID\_交换机\_端口\_已更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_UPDATED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)通知可扩展交换机扩展的可扩展交换机端口的参数正在更新。 仅将对端口，已创建，而尚未开始清除/删除进程发出 OID。 目前仅*PortFriendlyName*创建后受到更新字段。

可扩展交换机的协议边缘销毁以前的网络连接到的端口和端口的所有 OID 请求已都完成时发出此 OID 请求。

**请注意**  无法发出此 OID 请求，如果网络适配器已不以前连接到该端口。

 

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

<a href="" id="oid-switch-port-teardown"></a>[OID\_交换机\_端口\_拆解](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)通知可扩展交换机扩展的可扩展交换机端口正在被删除。 可扩展交换机的协议边缘销毁以前的网络连接到的端口和端口的所有 OID 请求已都完成时发出此 OID 请求。

**请注意**  无法发出此 OID 请求，如果网络适配器已不以前连接到该端口。

 

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

该扩展将转发此 OID 请求后，它可以不再 OID 的发出请求正在删除的端口。

<a href="" id="oid-switch-port-delete"></a>[OID\_交换机\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)  
可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)通知可扩展交换机扩展的可扩展交换机端口已被删除。 可扩展交换机的协议边缘后它会发出发出此 OID 请求[OID\_切换\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)请求和目标端口的 OID 请求已完成。

扩展始终将转发此可扩展交换机在驱动程序堆栈的下层的 OID 集请求。 扩展必须不会使请求失败。

创建用于网络连接分配的标识符大于所有可扩展交换机端口**NDIS\_切换\_默认\_端口\_ID**。 **NDIS\_交换机\_默认\_端口\_ID**标识符是保留的使用以下方式：

-   源端口数据包存储在数据包的带外 (OOB) 转发上下文与关联的标识符及其[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 源端口标识符**NDIS\_切换\_默认\_端口\_ID**指定数据包是否从可扩展的交换机扩展而不是从可扩展交换机端口。 源端口标识符的数据包**NDIS\_切换\_默认\_端口\_ID**是受信任并跳过的可扩展交换机端口策略，如访问控制列表 (Acl) 和服务质量 (QoS)。

    该扩展可能想要视为源自特定端口的数据包。 这样，该端口将应用于该数据包的策略。 扩展调用[ *SetNetBufferListSource* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)更改数据包的源端口。

    但是，可能有该扩展可能会的想要分配到的数据包的源端口标识符**NDIS\_交换机\_默认\_端口\_ID**。 例如，该扩展可能想要将源端口标识符设置为**NDIS\_交换机\_默认\_端口\_ID**为发送到设备的专有控制数据包外部网络。

    有关转发上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

-   对象的标识符 (OID) 请求[OID\_切换\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)颁发的可扩展交换机接口来封装的可扩展交换机外部颁发的 OID 请求网络适配器。 例如，硬件卸载 OID 请求封装由接口之前颁发下可扩展交换机驱动程序堆栈。

    扩展还可以颁发封装的 OID 请求才能转发下可扩展交换机控件路径的请求。 这允许扩展来查询或配置的基础物理网络适配器的功能。

    **InformationBuffer**的成员**NDIS\_OID\_请求**结构为此 OID 请求包含一个指向[ **NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构。 如果**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**，这将指定的 OID 请求是否来自可扩展交换机接口。 如果**DestinationPortId**设置为**NDIS\_交换机\_默认\_端口\_ID**，这将指定的目标 OID 请求通过可扩展交换机驱动程序堆栈中的扩展插件的处理。

    有关 OID 的请求的控制路径的详细信息，请参阅[HYPER-V 可扩展交换机控件路径，对于 OID 请求](hyper-v-extensible-switch-control-path-for-oid-requests.md)。

-   NDIS 状态迹象[ **NDIS\_状态\_切换\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)颁发的可扩展切换到的微型端口边缘封装可扩展交换机外部网络适配器从一个状态说明。

    扩展还可以颁发封装的 NDIS 状态指示才能转发向上可扩展交换机控制路径的迹象。 这允许扩展更改基础物理网络适配器的报告的功能。

    **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构，这种指示包含指向[ **NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。 如果**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**，这将指定的状态指示已发起由可扩展交换机接口。 如果**DestinationPortId**设置为**NDIS\_交换机\_默认\_端口\_ID**，这将指定的目标 OID 请求通过可扩展交换机驱动程序堆栈中的扩展插件的处理。

    有关 NDIS 状态指示的控制路径的详细信息，请参阅[HYPER-V 可扩展交换机控件路径，为 NDIS 状态指示](hyper-v-extensible-switch-control-path-for-ndis-status-indications.md)。

可扩展交换机接口维护每个端口都已创建一个引用计数器。 如果它的引用计数器具有非零值，将不会删除一个端口。 该接口用于递增或递减可扩展交换机端口的引用计数器提供了以下处理程序函数：

<a href="" id="referenceswitchport"></a>[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展将调用此函数可使端口的引用计数器递增。 虽然引用计数器有一个非零值，可扩展交换机的协议边缘不会发出的对象标识符 (OID) 组请求[OID\_切换\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)删除可扩展交换机端口。

扩展必须调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)之前执行任何操作都需要端口处于活动状态。 例如，扩展必须调用*ReferenceSwitchPort*它发出的 OID 方法请求之前[OID\_交换机\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum).

**请注意**  不能调用该扩展[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)端口收到 OID 后设置的请求[OID\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)为该端口。

 

<a href="" id="dereferenceswitchport"></a>[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)  
可扩展交换机扩展将调用此函数以减少端口的引用计数器。

扩展必须调用[ *DereferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)端口上所执行的操作完成后。 例如，如果该扩展调用*ReferenceSwitchPort*之前如果颁发[OID\_交换机\_端口\_属性\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)请求，扩展必须调用*DereferenceSwitchPort* OID 请求已完成后。

**请注意**  NDIS 端口和可扩展的交换机端口是不同的对象。 始终将通过可扩展交换机数据路径移动的数据包分配给的 NDIS 端口号**NDIS\_默认\_端口\_数**。 但是，数据包的源和目标可扩展交换机端口号可能的值**NDIS\_切换\_默认\_端口\_ID**或更高版本。 有关详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

 





