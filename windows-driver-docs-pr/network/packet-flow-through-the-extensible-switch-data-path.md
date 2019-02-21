---
title: 通过可扩展交换机数据路径的数据包流
description: 通过可扩展交换机数据路径的数据包流
ms.assetid: 9236CE95-F959-445F-849F-14377EE91D19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e74665598e19624152a1cc72075e5c5a6c57dd53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543140"
---
# <a name="packet-flow-through-the-extensible-switch-data-path"></a>通过可扩展交换机数据路径的数据包流


本主题介绍如何数据包将移到或从可扩展的交换机端口通过 HYPER-V 可扩展交换机数据路径。

**请注意**可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。



**请注意**此页面假定您熟悉中的信息[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。



从其端口到达可扩展交换机的所有数据包流量都遵循通过可扩展交换机驱动程序堆栈的相同路径。 例如，从外部网络适配器连接接收或发送从虚拟机 (VM) 网络适配器连接的数据包通信都将通过相同的数据路径。

下图显示了可扩展交换机数据路径 NDIS 6.40 (Windows Server 2012 R2) 和更高版本。

![关系图阐释超\-ndis 6.40 及更高版本的 v 可扩展交换机体系结构](images/vswitcharchitecture-ndis640.png)

下图显示可扩展交换机数据路径为 NDIS 6.30 (Windows Server 2012)。

![说明与 sr-iov 的合成设备数据路径的关系图](images/vswitcharchitecture.png)

有关可扩展交换机接口的组件的详细信息，请参阅[HYPER-V 可扩展交换机体系结构](hyper-v-extensible-switch-architecture.md)。

可扩展交换机数据路径具有以下部分中的数据包流通过它们的顺序列出：

-   [基础协议边缘](#overlying-protocol-edge)
-   [入口数据路径](#ingress-data-path)
-   [基础的微型端口边缘](#underlying-miniport-edge)
-   [出口数据路径](#egress-data-path)

### <a name="overlying-protocol-edge"></a>基础协议边缘

1.  数据包到达从已连接到交换机端口的网络适配器的可扩展交换机。 这些数据包首先发出从下可扩展交换机入口数据路径的可扩展交换机的协议边缘发送请求。

    可扩展交换机的协议边缘准备数据包的入口数据路径。 协议边缘为上下文区域分配包含带外 (OOB) 可扩展交换机转发上下文这些数据包。 它将填充从该数据包已传送到可扩展交换机的源端口和网络适配器连接有关的信息的 OOB 数据。

    有关转发上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

2.  如果数据包，NVGRE 数据包从外部网络适配器中 6.40 NDIS (Windows Server 2012 R2) 及更高版本，设置可扩展交换机**NativeForwardingRequired**中数据包的带外 (OOB) 信息的标志。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

3.  如果数据包到达的流量会出现在虚拟子网在端口上，设置可扩展交换机**VirtualSubnetId**的成员[ **NDIS\_NET\_缓冲区\_列表\_虚拟\_子网\_信息**](https://msdn.microsoft.com/library/windows/hardware/jj614359)数据包的结构。

    **请注意**虚拟子网可能是 HNV 子网或第三方虚拟子网。



### <a name="ingress-data-path"></a>入口数据路径

1.  扩展将从传入数据路径中获取一个数据包时其[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)调用函数。 该扩展将数据包转发到基础扩展的入口数据路径上通过调用[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)。 筛选和转发扩展还可以将数据包从删除的入口数据路径通过调用[ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)。

2.  当捕获扩展获得的入口数据路径上的数据包时，它们可以检查数据包数据。 但是，捕获扩展必须完成的入口数据路径上的数据包的发送请求。 这些扩展必须始终将数据包转发到可扩展交换机驱动程序堆栈中的基础扩展。

    捕获扩展还可以源自的入口数据路径上的数据包。 例如，该扩展可能来源中对报表到远程监视应用程序的交通状况的顺序的数据包。

    由扩展原始数据包的详细信息，请参阅[源自数据包流量](originating-packet-traffic.md)。

3.  筛选扩展获取入口数据路径上的数据包，它们可以执行以下操作：

    -   丢弃数据包基于自定义可扩展交换机或端口策略。

        有关这些策略的详细信息，请参阅[HYPER-V 可扩展交换机策略](hyper-v-extensible-switch-policies.md)。

        **请注意**获取入口数据路径上的数据包没有数据包的 OOB 数据中定义的目标端口。 因此，筛选扩展必须仅强制执行基于数据包数据或数据包的源端口或网络适配器连接的自定义策略。




-   克隆或修改从入口数据路径获取的数据包。

-   将新的数据包注入到入口数据路径。


4.  NDIS 6.40 及更高版本之后捕获和筛选扩展, 但之前的入口数据路径上的转发扩展，可扩展交换机执行以下操作：
    -   如果数据包是从外部网络适配器的 NVGRE 数据包，表示数据包标头中的地址是提供程序地址 (PA) 空间地址。 通过设置的可扩展交换机指明这**NativeForwardingRequired**中数据包的带外 (OOB) 信息的标志。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

    -   可扩展交换机适用于该数据包的内置入口策略。 这些策略可能包括入口的访问控制列表 (Acl)，DHCP 保护，并且路由器保护。

5.  如果未在可扩展交换机驱动程序堆栈启用转发扩展，由可扩展交换机确定数据包的目标端口数组。

6.  如果启用了转发扩展，它获取的入口数据路径上的数据包时必须执行以下操作：

    -   在 NDIS 6.40 及更高版本，如果数据包是 NVGRE 数据包 (请参阅[混合转发](hybrid-forwarding.md))，转发扩展不能修改入口数据路径中的数据包的 OOB 数据中的目标端口数组。 但是，它可以丢弃该数据包。

    -   如果数据包不是 NVGRE 数据包，转发扩展必须将目标端口添加到 OOB 数据中的数据包中的目标端口数组。

    -   转发扩展必须删除基于标准或自定义可扩展交换机或端口策略的数据包。 标准交换机或端口的策略包括安全和虚拟 LAN (VLAN) 属性。 如果在可扩展交换机驱动程序堆栈中不启用转发扩展，这些策略会强制执行可扩展交换机。

        **请注意**当转发扩展筛选器中的入口数据路径的数据包时，它将应用筛选规则根据源端口，以及该扩展将分配给该数据包的目标端口。




此外，转发扩展可以执行以下步骤：

-   克隆或修改从入口数据路径获取的数据包。

-   将新的数据包注入到入口数据路径。


### <a name="underlying-miniport-edge"></a>基础的微型端口边缘

1.  当数据包到达边缘基础微型端口的可扩展交换机时，可扩展交换机将适用于数据包其内置的策略。 这些策略包括访问控制列表 (Acl) 和质量的服务 (QoS) 属性。 如果由于这些策略不丢弃该数据包，可扩展交换机源自数据包的接收指示，并将转发数据包向上出口数据路径。

    **请注意**微型端口边缘的数据包将被传送到端口上启用端口镜像，如果将目标端口添加到镜像端口的数据包的 OOB 数据。 微型端口边缘执行而不考虑是否转发扩展已安装并启用可扩展交换机驱动程序堆栈中此操作。 微型端口边缘仅添加镜像端口，如果未指定数据包的目标端口数组中。



2.  如果未启用转发扩展，可扩展交换机确定数据包的目标端口，并将这些目标端口添加到包的 OOB 数据之前将转发数据包向上出口数据路径。

3.  NDIS 6.40 及更高版本，HNV 组件将执行任何所需的 NVGRE 封装或解封之后流入和流出量之前，以便转发扩展可以看到数据包中封装和解封窗体。 例如，如果数据包到达从外部网络适配器，且目标为内部 VM，转发扩展获取封装的数据按流入和出口上将解封的数据包。

    **请注意**中封装的数据包，表示数据包标头中的地址是提供程序地址 (PA) 空间地址。 在将解封的数据包，它是客户地址 (CA) 空间地址。



    1.  如果数据包 NVGRE 数据包到达从外部网络适配器，可扩展交换机的 HYPER-V 网络虚拟化 (HNV) 组件对数据包执行 NVGRE 解封。 HNV 组件确定 HNV 策略根据数据包的目标，然后可扩展交换机将向上出口数据路径的数据包。

    2.  如果数据包到达并且从内部 VM，HNV 组件将执行 NVGRE 封装数据包 HNV 策略设置为该数据包。 HNV 组件确定 HNV 策略根据数据包的目标，然后可扩展交换机将向上出口数据路径的数据包。

    3.  否则，转发扩展转发向上出口数据路径数据包。

4.  在 NDIS 6.30，如果启用转发扩展，则它必须将数据包转发向上出口数据路径。

### <a name="egress-data-path"></a>出口数据路径

1.  扩展将从出口数据路径中获取一个数据包时其[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)调用函数。 该扩展将数据包转发到通过调用过量的出口数据路径上的扩展[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)。 筛选和转发扩展还可以将数据包从删除出口数据路径通过调用[ **NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)。

2.  当转发扩展获得出口数据路径上的数据包时，它可以检查 OOB 数据中的数据包的目标端口信息。

    **请注意**扩展插件中获取此信息从 OOB 数据，通过调用[ *GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)。




根据标准或自定义的交换机或端口策略，该扩展可以排除数据包传递到 OOB 数据中包含的一个或多个目标端口。


3.  NDIS 6.40 (Windows Server 2012 R2) 及更高版本之后转发扩展, 但之前的筛选和捕获的出口数据路径上的扩展，可扩展交换机内置出口将策略应用于该数据包。 这些策略可能包括 trunk 模式下，监视模式、 出口 Acl 和质量 (QoS) 服务属性。

4.  当筛选扩展获得出口数据路径上的数据包时，它们可以检查 OOB 数据中的数据包的目标端口信息。 基于自定义的交换机或端口策略，该扩展可以排除数据包传递到 OOB 数据中包含的一个或多个目标端口。

    如果需要修改在包中的数据筛选扩展，必须先克隆数据包而无需保留端口的目标。 然后，该扩展必须将修改后的数据包注入到入口数据路径。 这允许修改数据包上强制实施策略的基础扩展并转发扩展可以添加端口的目标。

    有关详细信息，请参阅[克隆或数据包流量](cloning-or-duplicating-packet-traffic.md)。

5.  当捕获扩展获得出口数据路径上的数据包时，它们可以检查数据包数据。 但是，如果需要发起到远程监视应用程序到报表交通状况的顺序的数据包捕获扩展，它必须发起此数据包流量通过调用[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)以启动发送操作的入口数据路径上。

6.  当数据包到达边缘基础协议的可扩展交换机时，可扩展交换机接口将转发到指定的目标的所有端口的数据包。

7.  一旦已转发的数据包，接口将完成数据包通过按相反的顺序相同的路径。 首先，接口调用的扩展[ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)函数来完成出口数据路径上转发的数据包。 然后，该接口调用的扩展[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)函数来完成入口数据路径上转发的数据包。

    出口和入口数据路径上完成数据包时，该扩展不执行任何必要的数据包的清理和后期处理功能，可能需要。
