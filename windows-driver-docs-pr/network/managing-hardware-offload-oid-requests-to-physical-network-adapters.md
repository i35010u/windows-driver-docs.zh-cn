---
title: 管理发往物理网络适配器的硬件卸载 OID 请求
description: 管理发往物理网络适配器的硬件卸载 OID 请求
ms.assetid: A646CBB8-89AD-4C08-BECB-1E54E4D74311
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8d29d3593ad82218b2e98195dfe26c3b403f0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844123"
---
# <a name="managing-hardware-offload-oid-requests-to-physical-network-adapters"></a>管理发往物理网络适配器的硬件卸载 OID 请求


本主题讨论了如何通过可扩展交换机控制路径管理 Hyper-v 可扩展交换机转发扩展对底层物理适配器上的硬件卸载技术的对象标识符（OID）的请求。

例如，可以将外部网络适配器绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。

在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 管理可扩展交换机团队的转发扩展称为*组合提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了 NDIS 6.40 （Windows Server 2012 R2）和更高版本的可扩展交换机团队的示例。

![用于 ndis 6.40 的可扩展交换机团队示意图](images/vswitch-oid-controlpath2-ndis640.png)

下图显示了 NDIS 6.30 （Windows Server 2012）的可扩展交换机团队示例。

![用于 ndis 6.30 的可扩展交换机团队示意图](images/vswitch-oid-controlpath2.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

通过处理[oid\_SWITCH\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)的 oid 请求，转发扩展可以参与可扩展交换机团队的配置以实现硬件卸载。 例如，如果扩展管理可扩展交换机团队的物理网络适配器，则可以将 OID\_交换机\_\_NIC 转发到支持硬件卸载的物理适配器。

NDIS 和过量协议以及筛选器驱动程序可以向底层物理网络适配器发出对硬件卸载技术的 OID 请求。 当这些 OID 请求到达可扩展交换机接口时，它将在[**NDIS\_交换机\_NIC\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)中封装 oid 请求。 然后，可扩展交换机的协议边缘[\_NIC\_请求中\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)发出 oid 请求，该请求包含此结构。

可扩展交换机接口封装以下硬件卸载技术的 Oid：

<a href="" id="internet-protocol-security--ipsec--offload--version-2-"></a>Internet 协议安全（IPsec）卸载（版本2）  
以下 IPsec OID 请求被封装：

-   [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)

-   [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa-ex)

-   [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)

-   [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)

转发扩展不能*失败或拒绝*这些 OID 请求。

有关 IPsec 硬件卸载技术版本2的详细信息，请参阅[Ipsec 卸载版本 2](ipsec-offload-version-2.md)。

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>单个根 i/o 虚拟化（SR-IOV）  
以下 SR-IOV OID 请求被封装：

-   [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)

-   [OID\_NIC\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)

-   [OID\_NIC\_交换机\_DELETE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)

-   [OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)

-   [OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_接收\_筛选器\_移动\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)

转发扩展可以拒绝[oid\_nic 的 oid 请求\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)和[OID\_nic\_交换机\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)使用 NDIS\_状态的状态代码来完成请求，\_\_状态。 但是，扩展不能否决其他 SR-IOV OID 请求。

有关 SR-IOV 硬件卸载技术的详细信息，请参阅[单一根 I/o 虚拟化（sr-iov）](single-root-i-o-virtualization--sr-iov-.md)。

<a href="" id="virtualized-machine-queue--vmq-"></a>虚拟机队列（VMQ）  
以下 VMQ OID 请求被封装：

-   [OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)

-   [OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_接收\_筛选器\_可用\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

-   [OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)

-   [OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)

转发扩展可以拒绝[oid\_接收\_筛选器的 oid 请求\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)和[OID\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)\_通过以除 NDIS\_状态\_成功的状态代码来完成请求来设置\_筛选器。 但是，扩展不能否决其他 VMQ OID 请求。

有关 VMQ 硬件卸载技术的详细信息，请参阅[虚拟机队列（VMQ）](virtual-machine-queue--vmq-.md)。

转发扩展必须遵循以下准则来处理硬件卸载 OID 请求：

-   Microsoft IM 平台仅公布了整个团队的常见卸载功能。 但是，扩展可以生成 OID 请求，以查询团队中每个适配器的功能。

    一旦扩展确定了组中物理适配器的硬件功能，它就可以将硬件卸载的 OID 集请求转发到最适合卸载的适配器。

-   通过过量协议或筛选器驱动程序发出的所有硬件卸载 OID 请求都将封装在[**NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构中。 转发扩展发出的所有硬件卸载 OID 请求也必须封装在**NDIS\_交换机\_NIC\_OID\_请求**结构中。

    该扩展通过 oid [\_SWITCH\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)将封装的 oid 请求转发到基础物理网络适配器。 有关此过程的详细信息，请参阅[将 OID 请求转发到物理网络适配器](forwarding-oid-requests-to-physical-network-adapters.md)。

-   扩展不能修改或失败硬件卸载 OID 请求以清除、释放或完成卸载资源的分配。 例如，扩展不能[\_接收\_筛选器的 oid 请求失败，\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)或[oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)\_\_\_\_删除。 可扩展交换机接口必须处理这些 OID 请求，才能清理这些资源的状态信息。

    扩展可以修改或失败硬件卸载 OID 请求，以分配、移动或设置卸载资源。 例如，扩展可能会失败或修改[oid\_NIC 的 oid 请求\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)或[oid\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)\_\_\_IPSEC\_\_\_

-   此扩展可以从任何硬件卸载 Oid 到基础物理网络适配器。 但是，扩展不能产生清除或释放扩展未分配的卸载资源的硬件卸载 OID。

    例如，扩展不得产生 Oid 的硬件卸载 OID 请求[\_接收\_筛选器\_可用的\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)，前提是它不产生[oid\_接收\_筛选器\_为同一队列分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)请求。

    **请注意**  扩展在筛选过量驱动程序发出的同一 OID 请求时，只能产生自己的封装硬件卸载 OID 请求。 在这种情况下，扩展不能转发原始 OID 请求。 相反，该扩展插件必须调用[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete) ，以便在 NDIS 调用其[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)来完成发起的 OID 请求时完成此请求。

     

-   如果扩展插件将硬件卸载 OID 请求转发到基础物理网络适配器 **，则** [**NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构必须设置为该适配器的非零索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

    此外， **DestinationPortId**成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。

-   如果扩展插件正在为 Hyper-v 子分区分配资源，则必须将[**NDIS\_交换机\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)的**SourcePortId**成员设置为该分区连接到的可扩展交换机端口的标识符，然后才能将\_请求结构。

    必须将**SourceNicIndex**成员设置为**NDIS\_交换机\_默认\_NIC\_索引**。

-   当扩展调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)来转发 OID 请求时，它必须将*OidRequest*参数设置为指向[ **\_的 NDIS\_oid 请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 NDIS [\_\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)oid 请求的请求结构。

有关扩展如何筛选 OID 请求的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关 MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





