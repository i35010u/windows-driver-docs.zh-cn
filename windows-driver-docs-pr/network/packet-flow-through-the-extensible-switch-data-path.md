---
title: 通过可扩展交换机数据路径传输的数据包流
description: 通过可扩展交换机数据路径传输的数据包流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c53d9e4ae0ba6ee064340725ce04c9de63913ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840629"
---
# <a name="packet-flow-through-the-extensible-switch-data-path"></a>通过可扩展交换机数据路径传输的数据包流


本主题介绍如何通过 Hyper-v 可扩展交换机数据路径向可扩展交换机端口移入或移出包。

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅 [Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。



**注意**  本页假设你熟悉 [Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md) 和 [混合转发](hybrid-forwarding.md)概述中的信息。



从其端口到达可扩展交换机的所有数据包流量都遵循通过可扩展交换机驱动程序堆栈的相同路径。 例如，从外部网络适配器连接收到的数据包流量或从虚拟机 () VM 发送的数据包流量将通过相同的数据路径移动。

下图显示了 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机数据路径。

![说明 \- ndis 6.40 和更高版本的 hyper-v 可扩展交换机体系结构的示意图](images/vswitcharchitecture-ndis640.png)

下图显示了 NDIS 6.30 (Windows Server 2012) 的可扩展交换机数据路径。

![用 sr-iov 说明综合设备数据路径的示意图](images/vswitcharchitecture.png)

有关可扩展交换机接口的组件的详细信息，请参阅 [Hyper-v 可扩展交换机体系结构](hyper-v-extensible-switch-architecture.md)。

可扩展交换机数据路径具有以下部分，按数据包的传递顺序列出：

-   [过量协议边缘](#overlying-protocol-edge)
-   [入口数据路径](#ingress-data-path)
-   [基础微型端口边缘](#underlying-miniport-edge)
-   [出口数据路径](#egress-data-path)

### <a name="overlying-protocol-edge"></a>过量协议边缘

1.  数据包从连接到交换机端口的网络适配器到达可扩展交换机。 这些数据包首次作为发送请求从可扩展交换机的协议边缘向下发出发送请求。

    可扩展交换机的协议边缘准备入站数据路径的数据包。 协议边缘为包含带外 (OOB) 可扩展交换机转发上下文的数据包分配上下文区域。 它利用源端口和网络适配器连接的相关信息填充 OOB 数据，该连接将数据包传递到可扩展交换机。

    有关转发上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

2.  在 NDIS 6.40 (Windows Server 2012 R2) 及更高版本中，如果数据包是来自外部网络适配器的 NVGRE 数据包，则可扩展交换机会在数据包的带外 (OOB) 信息中设置 **NativeForwardingRequired** 标志。 有关详细信息，请参阅 [混合转发](hybrid-forwarding.md)。

3.  如果数据包到达流量有虚拟子网的端口，则可扩展交换机为该数据包设置 [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 虚拟 \_ 子网 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_virtual_subnet_info)结构的 **VirtualSubnetId** 成员。

    **注意**  虚拟子网可以是 HNV 子网，也可以是第三方虚拟子网。



### <a name="ingress-data-path"></a>入口数据路径

1.  调用 [*FilterSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists) 函数时，扩展会从入口数据路径获取数据包。 该扩展通过调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)将数据包转发到入口数据路径上的基础扩展。 筛选和转发扩展还可以通过调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)从入口数据路径中删除数据包。

2.  捕获扩展在入口数据路径上获取数据包时，它们可以检查数据包数据。 但是，捕获扩展不能完成发送数据路径上的数据包发送请求。 这些扩展必须始终将数据包转发到可扩展交换机驱动程序堆栈中的基础扩展。

    捕获扩展还可以在入口数据路径上产生数据包。 例如，扩展可能会产生数据包，以便向远程监视应用程序报告流量状态。

    若要详细了解如何通过扩展来发起数据包，请参阅 [原始数据包流量](originating-packet-traffic.md)。

3.  筛选扩展在入口数据路径上获取数据包时，可以执行以下操作：

    -   基于自定义的可扩展交换机或端口策略丢弃数据包。

        有关这些策略的详细信息，请参阅 [Hyper-v 可扩展交换机策略](hyper-v-extensible-switch-policies.md)。

        **注意**  在入口数据路径上获取的数据包在数据包的 OOB 数据中没有定义的目标端口。 因此，筛选扩展必须仅基于数据包数据或数据包的源端口或网络适配器连接强制执行自定义策略。




-   克隆或修改从入口数据路径获取的数据包。

-   将新包注入入入口数据路径。


4.  在 NDIS 6.40 和更高版本中，在捕获和筛选扩展之后但在入口数据路径上的转发扩展之前，可扩展交换机执行以下操作：
    -   如果数据包是来自外部网络适配器的 NVGRE 数据包，则数据包标头中的地址是提供程序地址 (PA) 空间地址。 可扩展交换机通过在数据包的带外 (OOB) 信息中设置 **NativeForwardingRequired** 标志来指示这一点。 有关详细信息，请参阅 [混合转发](hybrid-forwarding.md)。

    -   可扩展交换机将内置入口策略应用于数据包。 这些策略可能包括入口访问控制列表 (Acl) 、DHCP 防护和路由器防护。

5.  如果未在可扩展交换机驱动程序堆栈中启用转发扩展，则数据包的目标端口数组由可扩展交换机决定。

6.  如果启用了转发扩展，则它必须在入口数据路径上获取数据包时执行以下操作：

    -   在 NDIS 6.40 和更高版本中，如果数据包为 NVGRE 数据包 (参阅 [混合转发](hybrid-forwarding.md)) ，则转发扩展无法在入口数据路径中修改数据包的 OOB 数据中的目标端口数组。 但是，它可以删除该数据包。

    -   如果数据包不是 NVGRE 数据包，则转发扩展必须将目标端口添加到数据包的 OOB 数据中的目标端口数组。

    -   转发扩展必须基于标准或自定义的可扩展交换机或端口策略来删除数据包。 标准交换机或端口策略包括安全和虚拟 LAN (VLAN) 属性。 如果未在可扩展交换机驱动程序堆栈中启用转发扩展，则可扩展交换机将强制实施这些策略。

        **注意**  当转发扩展筛选入站数据路径中的数据包时，它将基于源端口以及扩展分配给数据包的目标端口应用筛选规则。




此外，转发扩展插件还可以执行以下操作：

-   克隆或修改从入口数据路径获取的数据包。

-   将新包注入入入口数据路径。


### <a name="underlying-miniport-edge"></a>基础微型端口边缘

1.  当数据包到达可扩展交换机的基础微型端口边缘时，可扩展交换机会将其内置策略应用于数据包。 这些策略包括访问控制列表 (Acl) 和服务质量 (QoS) 属性。 如果由于这些策略不会丢弃数据包，则可扩展交换机会为数据包发出接收指示，并在传出数据路径上转发包。

    **注意**  如果在要将数据包传递到的端口上启用端口镜像，则微型端口边缘会将目标端口添加到镜像端口的数据包的 OOB 数据。 不管是否在可扩展交换机驱动程序堆栈中安装并启用了转发扩展，小型端口边缘都将执行此功能。 小型端口边缘仅添加在数据包的目标端口数组中未指定的镜像端口。



2.  如果未启用转发扩展，则可扩展交换机会确定数据包的目标端口，并将这些目标端口添加到数据包的 OOB 数据，然后再将数据包转发到传出的数据路径。

3.  在 NDIS 6.40 和更高版本中，HNV 组件在进入后和传出之前执行任何所需的 NVGRE 封装或和解，以便转发扩展可以查看封装和解封格式的数据包。 例如，如果数据包从外部网络适配器接收，并且是发往内部 VM，则转发扩展会在入口上获取封装的数据包，并在出口上获取解封数据包。

    **注意**  在封装的数据包中，数据包标头中的地址是 (PA) 空间地址的提供程序地址。 在解封数据包中，它是 (CA) 空间地址的客户地址。



    1.  如果数据包是从外部网络适配器收到的 NVGRE 数据包，则可扩展交换机的 Hyper-v 网络虚拟化 (HNV) 组件在数据包上执行 NVGRE 和解。 HNV 组件根据 HNV 策略确定数据包的目标，然后可扩展交换机将数据包上移出传出的数据路径。

    2.  如果数据包从内部 VM 接收，则 HNV 组件将在数据包上执行 NVGRE 封装（如果为该数据包设置了 HNV 策略）。 HNV 组件根据 HNV 策略确定数据包的目标，然后可扩展交换机将数据包上移出传出的数据路径。

    3.  否则，转发扩展会将数据包上移出传出的数据路径。

4.  在 NDIS 6.30 中，如果启用了转发扩展，则必须将数据包上移出传出的数据路径。

### <a name="egress-data-path"></a>出口数据路径

1.  调用 [*FilterReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists) 函数时，扩展会从出口数据路径获取数据包。 该扩展通过调用 [**NdisFIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)将数据包转发到传出数据路径上的过量扩展。 筛选和转发扩展还可以通过调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)从出口数据路径中删除数据包。

2.  当转发扩展在出口数据路径上获取数据包时，它可以在 OOB 数据中检查数据包的目标端口信息。

    **注意**  此扩展通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)从 OOB 数据获取此信息。




根据标准或自定义的交换机或端口策略，扩展可以排除将数据包传递到包含在 OOB 数据中的一个或多个目标端口。


3.  在 NDIS 6.40 (Windows Server 2012 R2) 和更高版本中，在转发扩展之后但在出口和捕获传出数据路径上的扩展之前，可扩展交换机将内置出口策略应用于数据包。 这些策略可能包括干线模式、监视模式、传出 Acl 和服务质量 (QoS) 属性。

4.  当筛选扩展在出口数据路径上获取数据包时，它们可以在 OOB 数据中检查数据包的目标端口信息。 根据自定义交换机或端口策略，扩展可以排除将数据包传递到 OOB 数据中包含的一个或多个目标端口。

    如果筛选扩展需要修改数据包中的数据，则必须先克隆数据包，而不保留端口目标。 然后，该扩展插件必须将已修改的数据包注入入入口数据路径。 这允许基础扩展在已修改的数据包上强制实施策略，转发扩展可以添加端口目标。

    有关详细信息，请参阅 [克隆或数据包通信](cloning-or-duplicating-packet-traffic.md)。

5.  捕获扩展在出口数据路径上获取数据包时，它们可以检查数据包数据。 但是，如果捕获扩展需要产生数据包以便向远程监视应用程序报告流量条件，则它必须通过调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 以在入口数据路径上启动发送操作来产生此数据包流量。

6.  当数据包到达可扩展交换机的过量协议边缘时，可扩展交换机接口会将数据包转发到所有指定的目标端口。

7.  转发数据包后，接口将通过同一路径反向完成包。 首先，接口调用扩展的 [*FilterReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists) 函数来完成在出口数据路径上转发的数据包。 然后，接口调用扩展的 [*FilterSendNetBufferListsComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete) 函数来完成在入口数据路径上转发的数据包。

    当数据包在出口和入口数据路径上完成时，扩展将执行任何必要的数据包清理和可能需要的后期处理。
