---
title: 管理发往物理网络适配器的硬件卸载 OID 请求
description: 管理发往物理网络适配器的硬件卸载 OID 请求
ms.assetid: A646CBB8-89AD-4C08-BECB-1E54E4D74311
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68ea7bd874fc506ff77d57a6d82aef7480ea1727
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356181"
---
# <a name="managing-hardware-offload-oid-requests-to-physical-network-adapters"></a>管理发往物理网络适配器的硬件卸载 OID 请求


本主题讨论如何转发扩展的 HYPER-V 可扩展交换机管理对象标识符 (OID) 的硬件请求卸载基础物理适配器上的技术通过可扩展交换机控制路径。

例如，外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。

在此配置中，向团队中每个网络适配器公开可扩展交换机扩展。 这允许要管理的配置和使用的团队中的单个网络适配器的扩展。 例如，转发扩展可用于负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 管理可扩展交换机团队的转发扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了一个可扩展交换机团队 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的示例。

![ndis 6.40 可扩展交换机团队的关系图](images/vswitch-oid-controlpath2-ndis640.png)

下图显示的 NDIS 6.30 (Windows Server 2012) 的可扩展交换机团队的示例。

![ndis 6.30 可扩展交换机团队的关系图](images/vswitch-oid-controlpath2.png)

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*.

 

通过处理 OID 请求的[OID\_切换\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)，转发扩展可以参与可扩展交换机团队硬件卸载功能的配置。 例如，如果扩展可用于管理可扩展交换机团队的物理网络适配器，它可以转发 OID\_切换\_NIC\_请求支持硬件卸载的物理适配器的请求。

NDIS 和基础协议和筛选器驱动程序可以发出硬件卸载技术的 OID 请求到基础物理网络适配器。 当这些 OID 请求在可扩展交换机接口，它封装在 OID 请求[ **NDIS\_切换\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request). 然后，可扩展交换机的协议边缘颁发的 OID 请求[OID\_切换\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)，其中包含此结构。

可扩展交换机接口封装的以下硬件卸载技术 Oid:

<a href="" id="internet-protocol-security--ipsec--offload--version-2-"></a>Internet 协议安全 (IPsec) 卸载 （第 2 版）  
封装以下 IPsec OID 请求：

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa-ex)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)

转发扩展必须不会失败，或*否决权*，这些 OID 请求。

有关版本 2 的 IPsec 硬件卸载技术的详细信息，请参阅[IPsec 卸载版本 2](ipsec-offload-version-2.md)。

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>单根 I/O 虚拟化 (SR-IOV)  
封装以下 SR-IOV OID 请求：

-   [OID\_NIC\_SWITCH\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)

-   [OID\_NIC\_SWITCH\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)

-   [OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)

-   [OID\_NIC\_SWITCH\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)

-   [OID\_RECEIVE\_FILTER\_CLEAR\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_RECEIVE\_FILTER\_MOVE\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)

转发扩展可否决的 OID 请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)并[OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)通过完成请求状态代码以外 NDIS\_状态\_成功。 但是，该扩展不能阻止其他 SR-IOV OID 请求。

有关 SR-IOV 的硬件的卸载技术的详细信息，请参阅[单根 I/O 虚拟化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)。

<a href="" id="virtualized-machine-queue--vmq-"></a>虚拟的机队列 (VMQ)  
封装以下 VMQ OID 请求：

-   [OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)

-   [OID\_RECEIVE\_FILTER\_CLEAR\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)

-   [OID\_RECEIVE\_FILTER\_FREE\_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

-   [OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)

-   [OID\_RECEIVE\_FILTER\_SET\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)

转发扩展可否决的 OID 请求[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)并[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)通过完成请求状态代码以外 NDIS\_状态\_成功。 但是，该扩展不能阻止其他 VMQ OID 请求。

有关 VMQ 硬件的卸载技术的详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。

转发扩展必须遵循以下准则，以便处理硬件卸载 OID 请求：

-   Microsoft IM 平台播发卸载功能的整体团队仅常见。 但是，扩展可以生成 OID 请求，可查询的团队中每个适配器的性能。

    一旦扩展插件确定团队中的物理适配器的硬件功能，它可以将硬件卸载功能的 OID 集请求转发到最适合用于卸载的适配器。

-   由过量协议或筛选器驱动程序产生的所有硬件卸载 OID 请求将都封装在[ **NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构。 转发扩展就会生成的所有硬件卸载 OID 请求还必须都封装在**NDIS\_交换机\_NIC\_OID\_请求**结构。

    该扩展将封装的 OID 请求转发到通过 OID 集请求的基础物理网络适配器[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)。 此过程的详细信息，请参阅[转发到物理网络适配器的 OID 请求](forwarding-oid-requests-to-physical-network-adapters.md)。

-   扩展名不得修改或硬件卸载 OID 请求，若要清除，免费，失败或完成卸载资源分配。 例如，扩展必须成功的 OID 请求[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)或者[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)。 可扩展交换机接口必须处理这些 OID 请求，以清理这些资源的状态信息。

    该扩展可以修改或故障硬件卸载 OID 请求，以分配、 移动或集卸载资源。 例如，扩展可以故障或修改的 OID 请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)或者[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)。

-   该扩展可以源自任何硬件卸载 Oid 到基础物理网络适配器。 但是，该扩展必须不是源自硬件卸载功能的清除或释放的 OID 将卸载该扩展未分配的资源。

    例如，扩展不得源自的硬件卸载 OID 请求[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)如果它不是源自[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)同一个队列的请求。

    **请注意**  如果它正在筛选同一个 OID 请求已颁发的过量驱动程序，扩展仅可以由自己封装的硬件卸载 OID 的请求。 在这种情况下，该扩展不能转发原始 OID 请求。 相反，扩展必须调用[ **NdisFOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequestcomplete)若要完成此请求时 NDIS 调用其[ *FilterOidRequestComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)若要完成起源于的 OID 请求。

     

-   如果扩展将硬件卸载 OID 请求转发到基础物理网络适配器**DestinationNicIndex**的成员[ **NDIS\_开关\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构必须设置为非零的索引值的适配器。 有关这些索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

    此外， **DestinationPortId**成员必须设置为外部网络适配器连接到可扩展的交换机端口的标识符。

-   如果扩展原始的 HYPER-V 子分区中，为分配的资源的硬件卸载 OID 请求**SourcePortId**的成员[ **NDIS\_开关\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构必须设置为分区连接到可扩展的交换机端口的标识符。

    **SourceNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**。

-   当扩展调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest) OID 请求转发，它必须设置*OidRequest*参数指向的指针[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构[OID\_开关\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)OID 请求。

有关如何扩展筛选 OID 请求的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





