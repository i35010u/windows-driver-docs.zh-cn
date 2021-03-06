---
title: 接收 Hyper-v 可扩展交换机配置更改 OID 请求
description: 接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f464117c1bb7ac1105b548cf6c48e67fb1e4e20
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247817"
---
# <a name="receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes"></a>接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求

可扩展交换机接口通过颁发可扩展的交换机对象标识符 (OID) 设置请求，通知基础扩展。 这些请求由可扩展交换机的协议边缘颁发，通知基础扩展有关可扩展交换机组件配置和策略参数的更改。 这些 OID 请求在可扩展交换机驱动程序堆栈到可扩展交换机的基础微型端口边缘之间移动。

下图显示了 (Windows Server 2012 R2) 和更高版本的 NDIS 6.40 的 OID 请求的可扩展交换机控制路径。

![用于 ndis 6.40 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath-ndis640.png)

下图显示了 (Windows Server 2012) 的 NDIS 6.30 的 OID 请求的可扩展交换机控制路径。

![用于 ndis 6.30 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。 

可扩展交换机的协议边缘为以下类型的通知颁发 OID 集请求：

-   对可扩展交换机上端口配置的更改。

    例如，协议驱动程序会发出 [OID \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md) ，通知基础扩展有关在可扩展交换机上创建端口的信息。 同样，协议驱动程序会发出 [OID \_ 交换机 \_ 端口 \_ DELETE](./oid-switch-port-delete.md) ，通知有关删除端口的信息。

    有关此类型 OID 通知的详细信息，请参阅 [Hyper-v 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

-   将网络适配器连接到可扩展交换机上的端口。

    例如，协议驱动程序会发出 [OID \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md) ，通知有关网络适配器与可扩展交换机上端口的连接的基础扩展。 同样，协议驱动程序会发出 [OID \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md) ，通知扩展网络适配器已与端口断开连接。

    有关此类型 OID 通知的详细信息，请参阅 [Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

-   可扩展交换机端口或交换机策略的更改。

    例如，协议驱动程序发出 [OID \_ 开关 \_ 属性 \_ ADD](./oid-switch-property-add.md) ，以通知基础扩展添加了可扩展的 SWITCH 属性。 同样，协议驱动程序会发出 [OID \_ 交换机 \_ 端口 \_ 属性 \_ DELETE](./oid-switch-port-property-delete.md) ，通知有关删除端口属性的扩展。

    有关此类型 OID 通知的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

    **注意**  不会向扩展通知对由可扩展交换机的基础微型端口边缘管理的默认端口或交换机策略的更改。

-   保存或还原运行时端口数据。

    例如，协议驱动程序会发出 [OID \_ 交换机 \_ NIC \_ save](./oid-switch-property-add.md) ，通知底层扩展插件为可扩展交换机上的指定端口保存运行时数据。 在将 Hyper-v 状态保存或迁移到另一台主机时，会发出这些 Oid。 同样，协议驱动程序会发出 [OID \_ 交换机 \_ NIC \_ RESTORE](./oid-switch-nic-restore.md) ，以通知扩展运行时端口数据正在可扩展交换机上还原。

    有关此类型 OID 通知的详细信息，请参阅 [管理 Hyper-v 可扩展交换机 Run-Time 数据](managing-hyper-v-extensible-switch-run-time-data.md)。

可扩展交换机扩展微型端口驱动程序负责完成这些 OID 请求。 但是，对于某些可扩展的开关 OID 请求，基础扩展可能会失败，从而导致拒绝通知。 例如，当可扩展交换机协议驱动程序向筛选器驱动程序通知有关将在可扩展交换机上创建的新端口时，它会发出 oid [ \_ 交换机 \_ 端口 \_ CREATE](./oid-switch-port-create.md)的 oid 设置请求。 基础筛选或转发扩展可以通过完成 OID 请求来拒绝端口创建，状态 \_ 数据 \_ 不 \_ 接受。

如果为可扩展的 switch OID 请求调用了其 [*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) 函数，则可扩展交换机扩展必须遵循以下准则：

-   扩展不能修改 *OidRequest* 参数指向的任何数据。

-   对于某些可扩展的开关 OID 请求，扩展可以完成 OID 请求，但 \_ \_ 不接受状态数据 \_ 。 这会在为其发出 OID 请求的可扩展交换机组件上 vetoes 操作。

    例如，扩展可以完成 [OID \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md) 请求，状态 \_ 数据 \_ 不 \_ 被接受。 如果驱动程序无法满足网络连接正在创建的指定端口上的配置策略，则可能需要执行此操作。

    扩展可通过以下 Oid 以这种方式完成请求：

    -   [OID \_ 交换机 \_ NIC \_ 创建](./oid-switch-nic-create.md)

    -   [OID \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md)

    -   [OID \_ 交换机 \_ 端口 \_ 属性 \_ 添加](./oid-switch-port-property-add.md)

    -   [OID \_ 交换机 \_ 端口 \_ 属性 \_ 删除](./oid-switch-port-property-delete.md)

    -   [OID \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md)

    -   [OID \_ 开关 \_ 属性 \_ 添加](./oid-switch-property-add.md)

    -   [OID \_ 开关 \_ 属性 \_ 删除](./oid-switch-property-delete.md)

    -   [OID \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md)

-   如果扩展不能完成 OID 请求，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以将请求转发到可扩展交换机驱动程序堆栈。

    **注意**  驱动程序调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)之前，驱动程序必须调用 [**NdisAllocateCloneOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest) 来分配 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构，并将请求信息传输到新的结构。

    调用 [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) 函数时，扩展应监视 OID 请求的完成结果。 这允许该扩展来确定可扩展交换机组件上的操作是已成功完成还是由基础扩展否决。

    有关如何筛选和转发 OID 请求的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。


-   NDIS 和过量协议以及筛选器驱动程序可以向底层物理网络适配器发出对硬件卸载技术的 OID 请求。 这包括针对卸载技术的 OID 请求，如虚拟机队列 (VMQ) 、Internet 协议安全 (IPsec) 以及单个根 i/o 虚拟化 (SR-IOV) 。

    当这些 OID 请求到达可扩展交换机接口时，它将在 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)中封装 oid 请求。 然后，可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) 的 oid 请求，其中包含此结构。

-   可扩展的交换机转发扩展可为绑定到外部网络适配器的一个或多个物理适配器上的 NDIS 硬件卸载技术提供支持。 在此配置中，可扩展交换机外部网络适配器绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 中间驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

    在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 此类扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

    通过处理 [oid \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md)的 oid 请求，组合提供程序可参与适配器组的配置以进行硬件卸载。 例如，扩展可以生成其自己的 oid \_ 交换机 \_ NIC \_ 请求，以配置包含硬件卸载参数的物理适配器。

    有关如何处理 [oid \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) oid 请求的详细信息，请参阅 [将 Oid 请求转发到物理网络适配器](forwarding-oid-requests-to-physical-network-adapters.md)。

    **注意**  扩展筛选器驱动程序可以生成 [oid \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) 的 Oid 请求，将专用 oid 颁发给绑定到可扩展交换机外部网络适配器的任何物理适配器。

**注意**  当可扩展的 switch OID 请求处于挂起状态时，使用 [**NdisFRestartFilter**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter) 的堆栈重新启动请求将无法完成。 出于此原因，等待堆栈重新启动的扩展必须完成任何正在进行的 OID 请求。

有关可扩展交换机 OID 请求的控制路径的详细信息，请参阅 [OID 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。
