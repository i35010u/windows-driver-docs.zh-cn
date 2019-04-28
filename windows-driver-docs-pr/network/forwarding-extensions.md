---
title: 转发扩展
description: 转发扩展
ms.assetid: 7ABBB3F3-66F5-4651-8A5A-94940F3FD82D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9edee9cb08971a5cd6eeabb6511359f0fca5989
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347376"
---
# <a name="forwarding-extensions"></a>转发扩展


转发扩展已筛选的扩展，与相同的功能，但负责执行核心数据包转发和筛选的可扩展交换机的任务。 这些任务包括：

-   确定数据包的目标端口。

    **请注意**  目标端口，并将数据包转发数据包是否 NVGRE 数据包，确定可扩展交换机的 HYPER-V 网络虚拟化 (HNV) 组件。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

     

-   通过强制执行标准端口的策略，如安全、 配置文件或虚拟 LAN (VLAN) 策略筛选数据包。

    **请注意**  可扩展交换机仍执行基于内置策略的筛选。 这些策略包括访问控制列表 (Acl) 和服务质量 (QoS)。

     

**请注意**  转发扩展未安装和启用了可扩展的交换机中，如果交换机确定数据包的目标端口以及筛选器基于标准的端口设置的数据包。

 

在可扩展交换机扩展微型端口驱动程序中的出口和入口数据路径的分层立即转发扩展。 有关这些数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

转发扩展可以执行以下命令，并获得入口数据路径的数据包：

-   它可以筛选数据包流量和强制实施自定义和标准端口或切换通过可扩展交换机的数据包传递的策略。 当转发扩展筛选器中的入口数据路径的数据包时，则会应用基于源端口，以及该扩展将分配给该数据包的目标端口的筛选规则。

    由独立软件供应商 (ISV) 定义自定义策略。 标准策略由可扩展交换机接口定义。 通过 HYPER-V WMI 管理层管理属性设置为这些类型的策略。 使用这些属性设置的对象标识符 (OID) 请求通过配置转发扩展[OID\_交换机\_端口\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598278)并[OID\_交换机\_属性\_更新](https://msdn.microsoft.com/library/windows/hardware/hh598283)。

    可扩展交换机策略的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

-   它可以将新的、 已修改，或克隆数据包注入到入口数据路径。

    有关详细信息，请参阅[HYPER-V 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

-   它可以确定将数据包传递到一个或多个可扩展交换机目标端口。 这样，要将数据包传送的目标端口添加到可扩展交换机端口的转发扩展。

    有关如何添加目标端口的详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

转发扩展可以执行以下命令，并获得出口数据路径的数据包：

-   它可以筛选数据包流量和强制实施自定义和标准端口或切换通过可扩展交换机的数据包传递的策略。 转发扩展筛选器的出口数据路径中的数据包，它可以应用基于数据包的源或目标端口的筛选规则。

-   它可以排除数据包传递到一个或多个可扩展交换机目标端口。 这允许要排除的数据包传递到可扩展的交换机端口的转发扩展。

    有关如何排除的数据包发送到可扩展交换机端口的详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

    **请注意**  转发扩展时处理出口数据路径上的数据包只能排除的数据包发送。 该扩展仅可以添加或修改的入口数据路径上的数据包的目标端口。

     

-   它可以修改数据包数据。 如果转发扩展需要修改在包中的数据，必须先克隆该数据包之前它将分配端口的目标。 该数据包已分配的已修改和端口目标后，该扩展必须将修改后的数据包注入到出口数据路径。

    有关详细信息，请参阅[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)。

除了检查 OID 请求和 NDIS 状态指示，转发扩展可以执行以下操作：

-   可以将注入到可扩展交换机控制路径的 Oid 或 NDIS 状态指示。 这样，要创建或修改 Oid 和状态指示，并将其转发到或从基础物理网络适配器的转发扩展。

    例如，可扩展交换机外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 在主机上，MUX 中间驱动程序本身可以绑定到一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。

    在此配置中，可扩展交换机扩展公开到可扩展交换机团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 此类扩展被称为*组合的提供程序*。

    通过充当组合的提供程序，转发扩展可以创建或修改 OID 请求启用或禁用在团队中的适配器上的硬件能力。 组合的提供程序还可以创建或修改基于更改团队中的一个或多个适配器的 NDIS 状态指示。

    有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

-   它可以通过返回状态来禁止创建可扩展交换机端口或网络适配器连接\_数据\_不\_接受适用的可扩展交换机 Oid。 例如，转发扩展可通过返回状态否决的端口创建请求\_数据\_不\_时，驱动程序收到 OID 集请求的接受[OID\_交换机\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)。

    **请注意**  转发扩展，请勿创建或删除端口或网络适配器连接。 可扩展交换机的协议边缘会发出通知有关创建或删除的端口或网络适配器连接的基础扩展的 Oid。 有关详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)。

     

-   有权添加或更新可扩展交换机或端口策略决策通过返回状态\_数据\_不\_接受适用的可扩展交换机 Oid。 例如，转发扩展有权添加端口策略决策通过返回状态\_数据\_不\_时，驱动程序收到 OID 集请求的接受[OID\_交换机\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)。

    有关可扩展交换机策略的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

转发扩展具有以下要求：

-   转发扩展必须作为支持可扩展交换机接口的 NDIS 筛选器驱动程序开发。

    有关筛选器驱动程序的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)。

    有关如何编写一个转发扩展的详细信息，请参阅[编写的 HYPER-V 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

-   适用于转发扩展的 INF 文件必须为修改的筛选器驱动程序安装该扩展。 NDIS 监视筛选器驱动程序不能安装在可扩展交换机驱动程序堆栈。

    有关修改筛选器驱动程序的详细信息，请参阅[类型的筛选器驱动程序](types-of-filter-drivers.md)。

    修改筛选器驱动程序的 INF 要求的详细信息，请参阅[配置修改筛选器驱动程序 INF 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   **FilterClass**值 INF 文件中的扩展必须设置为**ms\_切换\_向前**。 有关详细信息，请参阅[INF 的 HYPER-V 可扩展交换机扩展的要求](inf-requirements-for-hyper-v-extensions.md)。

-   可以在可扩展交换机的每个实例的驱动程序堆栈中启用只有一个转发扩展。

有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

有关转发扩展的详细信息，请参阅以下页面：

-   [组合提供程序扩展](teaming-provider-extensions.md)
-   [混合转发](hybrid-forwarding.md)

## <a name="related-topics"></a>相关主题


[将数据包转发到的 HYPER-V 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)

[将数据包转发到物理网络适配器](forwarding-packets-to-physical-network-adapters.md)

[HYPER-V 可扩展交换机的概述](overview-of-the-hyper-v-extensible-switch.md)

 

 






