---
title: 筛选扩展
description: 筛选扩展
ms.assetid: EDE50213-DFA0-4D8B-9E15-12AED8FDE5CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6474dd4ba003fd7ae3b991793c58b266e23c6eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353344"
---
# <a name="filtering-extensions"></a>筛选扩展


筛选扩展的 HYPER-V 可扩展交换机可以检查、 修改和可扩展交换机数据路径中插入数据包。 基于可扩展交换机端口和交换机策略设置，该扩展可以丢弃数据包或排除其交付到一个或多个目标端口。

捕获扩展中的入口数据路径之后和出口数据路径中的转发扩展之后调用筛选扩展。 有关这些数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

筛选扩展可以执行以下命令，并获得入口数据路径的数据包：

-   筛选数据包流量和强制实施自定义端口或切换通过可扩展交换机的数据包传递的策略。 筛选扩展筛选器中的入口数据路径的数据包，它可以应用筛选规则仅根据数据包的起源的源端口和网络适配器连接。 此信息存储在带外 (OOB) 数据的一个数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构并且可以通过使用获取[ **NET\_缓冲区\_列表\_交换机\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。

    **请注意**获取入口数据路径上的数据包不包含目标端口。 可以仅在获得出口数据路径上的数据包筛选基于目标端口的数据包。

    由独立软件供应商 (ISV) 定义自定义策略。 通过 HYPER-V WMI 管理层管理有关此策略类型的属性设置。 筛选扩展配置的对象标识符 (OID) 请求通过这些属性设置[OID\_交换机\_端口\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)和[OID\_交换机\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)。

    有关自定义可扩展端口或交换机策略的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

    **请注意**仅转发扩展可强制实施通过可扩展交换机的数据包发送的标准端口策略。

-   将新的、 已修改，或克隆数据包注入到入口数据路径。

    有关详细信息，请参阅[HYPER-V 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

筛选扩展可以执行以下命令，并获得出口数据路径的数据包：

-   筛选数据包流量和强制实施自定义端口或切换通过可扩展交换机的数据包传递的策略。 筛选扩展筛选器的出口数据路径中的数据包，它可以应用基于数据包的源或目标端口的筛选规则。 目标端口数据存储在数据包的 OOB 数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 扩展插件获取此信息通过调用[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数。

-   排除数据包传递到一个或多个可扩展交换机目标端口。 这允许要排除的数据包传递到可扩展的交换机端口的筛选扩展。

    有关如何排除的数据包发送到可扩展交换机端口的详细信息，请参阅[可扩展交换机目标端口不包括数据包传递](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

-   管理是通过推迟的出口数据路径上的数据包转发到一个或多个目标端口的通信流。

    例如，一个支持质量 (QoS) 服务的功能的筛选扩展插件可能想要立即调用[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)转发指定具有较高的数据包优先级值。 根据具体的流量流，该扩展可能想要在更高版本时转发的数据包，其中的较低的优先级值。

-   修改数据包数据。 如果需要修改在包中的数据筛选扩展，必须先克隆数据包而无需保留端口的目标。 然后，该扩展必须将修改后的数据包注入到入口数据路径。 这允许修改数据包上强制实施策略的基础扩展并转发扩展可以添加端口的目标。

    有关详细信息，请参阅[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)。

除了检查 OID 请求和 NDIS 状态指示，筛选扩展可以执行以下操作：

-   通过返回状态来禁止创建可扩展交换机端口或网络适配器连接\_数据\_不\_接受适用的可扩展交换机 Oid。 例如，筛选扩展可通过返回状态否决的端口创建请求\_数据\_不\_时，驱动程序收到 OID 集请求的接受[OID\_开关\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)。

    **请注意**筛选扩展不要创建或删除端口或网络适配器连接。 可扩展交换机的协议边缘发出 Oid 以通知有关创建或删除的端口或网络适配器连接基础的筛选器驱动程序。 有关详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)。

-   通过返回状态来添加或更新可扩展交换机或端口策略禁止\_数据\_不\_接受适用的可扩展交换机 Oid。 例如，筛选扩展有权添加端口策略决策通过返回状态\_数据\_不\_时在扩展插件接收的 OID 集请求接受[OID\_交换机\_端口\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)。

    有关可扩展交换机策略的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

筛选扩展具有以下要求：

-   筛选扩展必须作为支持可扩展交换机接口的 NDIS 筛选器驱动程序开发。

    有关筛选器驱动程序的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)。

    有关如何编写筛选扩展的详细信息，请参阅[编写的 HYPER-V 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

    **请注意**Windows 筛选平台 (WFP) 提供了筛选扩展 (Wfplwfs.sys) 框中可扩展交换机。 该扩展允许 WFP 筛选器或标注驱动程序来截获的 HYPER-V 可扩展交换机数据路径上的数据包。 这允许筛选器或标注驱动程序来执行数据包检查或修改使用 WFP 管理和系统函数。 有关 WFP 的概述，请参阅[Windows 筛选平台](porting-packet-processing-drivers-and-apps-to-wfp.md)。

-   筛选扩展的 INF 文件必须为修改的筛选器驱动程序安装该驱动程序。 NDIS 监视筛选器驱动程序不能安装在可扩展交换机驱动程序堆栈。

    有关修改筛选器驱动程序的详细信息，请参阅[类型的筛选器驱动程序](types-of-filter-drivers.md)。

    修改筛选器驱动程序的 INF 要求的详细信息，请参阅[配置修改筛选器驱动程序 INF 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   **FilterClass**值 INF 文件中的筛选器驱动程序必须设置为**ms\_切换\_筛选器**。 有关详细信息，请参阅[INF 的 HYPER-V 可扩展交换机扩展的要求](inf-requirements-for-hyper-v-extensions.md)。

-   可以绑定并启用了可扩展交换机的每个实例在驱动程序堆栈中任意数量的筛选扩展。 默认情况下，多个筛选扩展排序基于安装时。 例如，多个筛选扩展已分层在可扩展交换机驱动程序堆栈中使用最近安装的扩展在堆栈中的其他筛选扩展的上面。

    它们是绑定，可扩展交换机实例中启用后，可以重新排序筛选扩展可扩展交换机驱动程序堆栈中的分层。 有关详细信息，请参阅[重新排序的 HYPER-V 可扩展交换机扩展](reordering-hyper-v-extensibility-switch-extensions.md)。