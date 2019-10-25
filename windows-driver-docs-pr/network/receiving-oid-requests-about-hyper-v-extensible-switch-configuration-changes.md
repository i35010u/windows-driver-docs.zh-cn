---
title: 接收 Hyper-v 可扩展交换机配置更改 OID 请求
description: 接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求
ms.assetid: 9149BFF3-59B3-4563-A1A1-34FDD115964E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee0675e0e58118dbcd3d77941533d705e37ca5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842107"
---
# <a name="receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes"></a>接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求

可扩展交换机接口通过发出可扩展的交换机对象标识符（OID）设置请求，通知基础扩展有关可扩展交换机组件配置和策略参数的更改。 这些请求由可扩展交换机的协议边缘颁发，通知基础扩展有关可扩展交换机组件配置和策略参数的更改。 这些 OID 请求在可扩展交换机驱动程序堆栈到可扩展交换机的基础微型端口边缘之间移动。

下图显示了适用于 NDIS 6.40 的 OID 请求的可扩展交换机控制路径（Windows Server 2012 R2）和更高版本。

![用于 ndis 6.40 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath-ndis640.png)

下图显示了 NDIS 6.30 （Windows Server 2012）的 OID 请求的可扩展交换机控制路径。

![用于 ndis 6.30 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath.png)

**注意** 在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 

可扩展交换机的协议边缘为以下类型的通知颁发 OID 集请求：

-   对可扩展交换机上端口配置的更改。

    例如，协议驱动程序发出[OID\_交换机\_端口\_"创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)"，通知基础扩展有关在可扩展交换机上创建端口的信息。 同样，协议驱动程序会发出[OID\_交换机\_端口\_"删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)"，通知有关删除端口的扩展。

    有关此类型 OID 通知的详细信息，请参阅[Hyper-v 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

-   将网络适配器连接到可扩展交换机上的端口。

    例如，协议驱动程序[\_NIC 发出 OID\_交换机\_连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)，通知有关网络适配器与可扩展交换机上端口的连接的基础扩展。 同样，协议驱动程序会发出[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)，通知扩展网络适配器已与端口断开连接。

    有关此类型 OID 通知的详细信息，请参阅[Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

-   可扩展交换机端口或交换机策略的更改。

    例如，协议驱动程序发出[OID\_SWITCH\_属性\_"添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)"，通知基础扩展有关添加可扩展的 SWITCH 属性的信息。 同样，协议驱动程序会发出[OID\_交换机\_端口\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete) ，以通知有关删除端口属性的扩展。

    有关此类型 OID 通知的详细信息，请参阅[管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

    **注意** 不会向扩展通知对由可扩展交换机的基础微型端口边缘管理的默认端口或交换机策略的更改。

-   保存或还原运行时端口数据。

    例如，协议驱动程序发出[OID\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)，通知基础扩展插件为可扩展交换机上的指定端口保存运行时数据。 在将 Hyper-v 状态保存或迁移到另一台主机时，会发出这些 Oid。 同样，协议驱动程序会发出[OID\_交换机\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)，通知扩展在可扩展交换机上正在还原运行时端口数据。

    有关此类型 OID 通知的详细信息，请参阅[管理 Hyper-v 可扩展交换机运行时数据](managing-hyper-v-extensible-switch-run-time-data.md)。

可扩展交换机扩展微型端口驱动程序负责完成这些 OID 请求。 但是，对于某些可扩展的开关 OID 请求，基础扩展可能会失败，从而导致拒绝通知。 例如，当可扩展交换机协议驱动程序通知有关将在可扩展交换机上创建的新端口的筛选器驱动程序时，它会发出 oid [\_switch\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)的 oid 集请求\_CREATE。 基础筛选或转发扩展可以通过完成 OID 请求来拒绝端口创建，状态\_数据\_不\_接受。

如果为可扩展的 switch OID 请求调用了其[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数，则可扩展交换机扩展必须遵循以下准则：

-   扩展不能修改*OidRequest*参数指向的任何数据。

-   对于某些可扩展的开关 OID 请求，扩展可以用状态\_\_不\_接受的数据来完成 OID 请求。 这会在为其发出 OID 请求的可扩展交换机组件上 vetoes 操作。

    例如，扩展可以完成[OID\_交换机\_NIC\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)请求，但状态\_数据\_未被接受。 如果驱动程序无法满足网络连接正在创建的指定端口上的配置策略，则可能需要执行此操作。

    扩展可通过以下 Oid 以这种方式完成请求：

    -   [OID\_交换机\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)

    -   [OID\_交换机\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)

    -   [OID\_SWITCH\_端口\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)

    -   [OID\_SWITCH\_端口\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)

    -   [OID\_交换机\_端口\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)

    -   [OID\_SWITCH\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)

    -   [OID\_SWITCH\_属性\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)

    -   [OID\_SWITCH\_属性\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)

-   如果扩展不能完成 OID 请求，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以将请求转发到可扩展交换机驱动程序堆栈。

    **注意** 驱动程序调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)之前，驱动程序必须调用[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest) ，以[ **\_请求结构分配 NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) ，并将请求信息传输到新的结构。

    调用[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)函数时，扩展应监视 OID 请求的完成结果。 这允许该扩展来确定可扩展交换机组件上的操作是已成功完成还是由基础扩展否决。

    有关如何筛选和转发 OID 请求的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。


-   NDIS 和过量协议以及筛选器驱动程序可以向底层物理网络适配器发出对硬件卸载技术的 OID 请求。 这包括对卸载技术（例如虚拟机队列（VMQ）、Internet 协议安全（IPsec）和单根 i/o 虚拟化（SR-IOV））的 OID 请求。

    当这些 OID 请求到达可扩展交换机接口时，它将在[**NDIS\_交换机\_NIC\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)中封装 oid 请求。 然后，可扩展交换机的协议边缘[\_NIC\_请求中\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)发出 oid 请求，该请求包含此结构。

-   可扩展的交换机转发扩展可为绑定到外部网络适配器的一个或多个物理适配器上的 NDIS 硬件卸载技术提供支持。 在此配置中，可扩展交换机外部网络适配器绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 中间驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅[物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

    在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 此类扩展称为*组合提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

    通过处理[oid\_交换机的 oid 请求\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)，组合提供程序可参与适配器组的配置以进行硬件卸载。 例如，扩展可以\_NIC\_请求中生成自己\_的 oid oid 请求，以配置包含硬件卸载参数的物理适配器。

    有关如何处理[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)oid 请求的详细信息，请参阅[将 oid 请求转发到物理网络适配器](forwarding-oid-requests-to-physical-network-adapters.md)。

    **注意** 扩展筛选器驱动程序可以[\_交换机\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)生成 oid 请求，\_请求将专用 oid 颁发给绑定到可扩展交换机外部网络适配器的任何物理适配器。

**注意** 当可扩展的 switch OID 请求处于挂起状态时，使用[**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter)的堆栈重新启动请求将无法完成。 出于此原因，等待堆栈重新启动的扩展必须完成任何正在进行的 OID 请求。

有关可扩展交换机 OID 请求的控制路径的详细信息，请参阅[OID 请求的 Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path-for-oid-requests.md)。









