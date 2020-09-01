---
title: 转发扩展
description: 转发扩展
ms.assetid: 7ABBB3F3-66F5-4651-8A5A-94940F3FD82D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b6fd7c9d25d96b66ded17ba2c3bd628354a12d2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206105"
---
# <a name="forwarding-extensions"></a>转发扩展


转发扩展与筛选扩展具有相同的功能，但负责执行可扩展交换机的核心数据包转发和筛选任务。 这些任务包括以下内容：

-   确定数据包的目标端口。

    **注意**   如果数据包为 NVGRE 数据包，则可扩展交换机的 Hyper-v 网络虚拟化 (HNV) 组件决定目标端口并转发数据包。 有关详细信息，请参阅 [混合转发](hybrid-forwarding.md)。

     

-   通过强制实施标准端口策略来筛选数据包，如安全性、配置文件或虚拟 LAN (VLAN) 策略。

    **注意**   可扩展交换机仍根据内置策略执行筛选。 这些策略包括 (Acl) 和服务质量 (QoS) 的访问控制列表。

     

**注意**   如果未在可扩展交换机中安装和启用转发扩展，则交换机会确定数据包的目标端口，并根据标准端口设置筛选数据包。

 

转发扩展在出口和入口数据路径的可扩展交换机扩展微型端口驱动程序的紧上方。 有关这些数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

转发扩展可对在入口数据路径上获取的数据包执行以下操作：

-   它可以筛选数据包流量，并强制实施自定义和标准端口，或者通过可扩展交换机进行数据包传递的交换机策略。 当转发扩展筛选入站数据路径中的数据包时，它将基于源端口以及扩展分配给数据包的目标端口应用筛选规则。

    自定义策略是由独立软件供应商 (ISV) 定义的。 标准策略由可扩展交换机接口定义。 这些类型的策略的属性设置通过 Hyper-v WMI 管理层进行管理。 通过对象标识符，使用以下属性设置来配置转发扩展： oid [ \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md) 和 [oid \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md) (oid) 请求。

    有关可扩展交换机策略的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

-   它可以将新的、经过修改的或克隆的数据包注入到入口数据路径中。

    有关详细信息，请参阅 [Hyper-v 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

-   它可以确定将数据包传递到一个或多个可扩展交换机目标端口。 这允许转发扩展添加目标端口，以便将数据包传递到可扩展交换机端口。

    有关如何添加目标端口的详细信息，请参阅 [将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

转发扩展可对在出口数据路径上获取的数据包执行以下操作：

-   它可以筛选数据包流量，并强制实施自定义和标准端口，或者通过可扩展交换机进行数据包传递的交换机策略。 当转发扩展筛选出口数据路径中的数据包时，它可以根据数据包的源或目标端口应用筛选规则。

-   它可以排除数据包到一个或多个可扩展交换机目标端口的传送。 这允许转发扩展插件排除数据包到可扩展交换机端口的传送。

    有关如何将数据包传递到可扩展交换机端口的详细信息，请参阅 [排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

    **注意**   转发扩展在处理出口数据路径上的数据包时，只能排除数据包传送。 扩展只能在入口数据路径上添加或修改数据包的目标端口。

     

-   它可以修改数据包数据。 如果转发扩展需要修改数据包中的数据，则必须先克隆数据包，然后再分配端口目标。 修改数据包并分配端口目标后，扩展必须将已修改的数据包注入传出数据路径。

    有关详细信息，请参阅 [克隆数据包通信](cloning-or-duplicating-packet-traffic.md)。

除了检查 OID 请求和 NDIS 状态指示，转发扩展还可以执行以下操作：

-   它可以将 Oid 或 NDIS 状态指示注入可扩展交换机控制路径。 这允许转发扩展创建或修改 Oid 和状态指示，并将其转发到基础物理网络适配器或从基础物理网络适配器转发它们。

    例如，可扩展交换机外部网络适配器可以绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 中间驱动程序本身可以绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。

    在此配置中，可扩展交换机扩展会公开给可扩展交换机团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 此类扩展称为 *组合提供程序*。

    转发扩展可通过充当分组提供程序来创建或修改 OID 请求，以在组中的适配器上启用或禁用硬件功能。 组合提供程序还可以根据组中一个或多个适配器的更改来创建或修改 NDIS 状态指示。

    有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

-   它通过返回 \_ \_ 适用的可扩展交换机 OID 的状态数据，可以拒绝创建可扩展交换机端口或网络适配器连接 \_ 。 例如， \_ \_ \_ 当驱动程序收到 [oid \_ 交换机 \_ 端口 \_ CREATE](./oid-switch-port-create.md)的 oid 设置请求时，转发扩展可以通过返回不被接受的状态数据来拒绝端口创建请求。

    **注意**   转发扩展不会创建或删除端口或网络适配器连接。 可扩展交换机的协议边缘会发出 Oid，通知基础扩展有关创建或删除端口或网络适配器连接的信息。 有关详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)。

     

-   它通过返回 \_ \_ 适用的可扩展交换机 OID 的状态数据，可以拒绝添加或更新可扩展交换机或端口策略 \_ 。 例如， \_ \_ \_ 当驱动程序收到 [oid \_ 交换机 \_ 端口 \_ 属性 " \_ 添加](./oid-switch-port-property-add.md)" 的 oid 设置请求时，转发扩展可以通过返回不被接受的状态数据来拒绝端口策略的添加。

    有关可扩展交换机策略的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

转发扩展具有以下要求：

-   转发扩展必须开发为支持可扩展交换机接口的 NDIS 筛选器驱动程序。

    有关筛选器驱动程序的详细信息，请参阅 [NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)。

    有关如何编写转发扩展的详细信息，请参阅 [编写 Hyper-v 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

-   转发扩展的 INF 文件必须将扩展安装为修改筛选器驱动程序。 NDIS 监视筛选器驱动程序不能安装在可扩展交换机驱动程序堆栈中。

    有关修改筛选器驱动程序的详细信息，请参阅 [筛选器驱动程序的类型](types-of-filter-drivers.md)。

    有关修改筛选器驱动程序的 INF 要求的详细信息，请参阅 [配置修改筛选器驱动程序的 Inf 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   必须将扩展的 INF 文件中的 **FilterClass** 值设置为 **ms \_ 切换 \_ **。 有关详细信息，请参阅 [Hyper-v 可扩展交换机扩展的 INF 要求](inf-requirements-for-hyper-v-extensions.md)。

-   对于可扩展交换机的每个实例，驱动程序堆栈中只能启用一个转发扩展。

有关可扩展交换机团队的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

有关转发扩展的详细信息，请参阅以下页面：

-   [组合提供程序扩展](teaming-provider-extensions.md)
-   [混合转发](hybrid-forwarding.md)

## <a name="related-topics"></a>相关主题


[将数据包转发到 Hyper-V 可扩展交换机端口](forwarding-packets-to-hyper-v-extensible-switch-ports.md)

[将数据包转发到物理网络适配器](forwarding-packets-to-physical-network-adapters.md)

[Hyper-V 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)

 

