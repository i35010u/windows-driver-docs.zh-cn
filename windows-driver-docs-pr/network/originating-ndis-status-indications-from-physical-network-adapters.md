---
title: 从物理网络适配器发起 NDIS 状态指示
description: 从物理网络适配器发起 NDIS 状态指示
ms.assetid: D588CD7E-98A3-4BA8-A467-6492DA2186CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9a65f56229bb38114cf9f5d6fc7a58cf34d83ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843760"
---
# <a name="originating-ndis-status-indications-from-physical-network-adapters"></a>从物理网络适配器发起 NDIS 状态指示


本主题讨论可扩展交换机转发扩展插件为连接到交换机的网络适配器发起 NDIS 状态指示所使用的方法。 扩展可以针对以下类型的适配器发起 NDIS 状态指示：

-   绑定到可扩展交换机的[外部网络适配器](external-network-adapters.md)的一个或多个基础物理适配器。

    例如，可以将外部网络适配器绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。

    在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 管理可扩展交换机团队的转发扩展称为*组合提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

-   在 Hyper-v 子分区内公开并连接到可扩展交换机端口的虚拟机（VM）网络适配器。

下图显示了适用于 NDIS 6.40 （Windows Server 2012 R2）和更高版本的物理和 VM 网络适配器的 NDIS 状态指示的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.40 和更高版本的物理和 vm 网络适配器中的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath3-ndis640.png)

下图显示了 NDIS 6.30 （Windows Server 2012）的物理和 VM 网络适配器的 NDIS 状态指示的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.30 的物理和 vm 网络适配器的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath3.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

转发扩展可将封装的硬件卸载状态指示发送到可扩展交换机驱动程序堆栈中的过量驱动程序。 这也允许该扩展插件更改绑定到可扩展交换机外部网络适配器的物理适配器的底层团队的当前卸载功能。 当适配器组绑定到外部网络适配器时，仅将团队的常见功能播发到 NDIS 或过量的协议和筛选器驱动程序。 扩展可以通过将封装的状态指示起源到团队中某些适配器支持的播发功能来扩展播发功能。 例如，扩展可以发出封装的[**NDIS\_状态\_接收\_筛选器\_当前\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-filter-current-capabilities)指示更改整个团队的当前启用的接收筛选器功能。

**请注意**  仅转发扩展可能产生封装的状态指示。 有关此类型的扩展的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

 

通常情况下，转发扩展会产生封装的 NDIS 状态指示，以更改基础物理适配器的播发硬件卸载功能。 例如，扩展可能会产生以下类型的硬件卸载的状态指示：

-   Internet 协议安全（IPsec）。

-   虚拟机队列（VMQ）。

-   单根 I/O 虚拟化 (SR-IOV)。

转发扩展还可以发起封装的 NDIS 状态指示，以更改为 Hyper-v 子分区分配的硬件卸载资源。 从 NDIS 6.30 开始，扩展可以[ **\_交换机\_端口发出封装的 NDIS\_状态，\_删除\_VF**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-port-remove-vf)指示，以删除 VM 网络适配器与 PCI Express （PCIe）虚拟功能（VF）之间的绑定。 VF 由支持[单根 i/o 虚拟化（sr-iov）](single-root-i-o-virtualization--sr-iov-.md)接口的底层物理网络适配器公开和支持。

如果转发扩展插件为基础物理适配器的硬件卸载资源发出了一个封装的 NDIS 状态指示，则必须按以下方式将[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的成员设置为：

-   必须将**DestinationPortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**。
-   **DestinationNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**

-   **SourcePortId**成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。

-   必须将**SourceNicIndex**成员设置为**NDIS\_交换机\_默认\_NIC\_索引**。 这允许将状态指示解释为来自绑定到外部网络适配器的整个可扩展交换机团队。

    **请注意**  如果只有一个物理网络适配器绑定到外部网络适配器，则转发扩展还必须将此成员设置为**NDIS\_交换机\_默认\_NIC\_索引**。

     

-   **StatusIndication**成员必须设置为指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。 此结构包含封装的 NDIS 状态指示的数据。

如果转发扩展插件为 Hyper-v 子分区的硬件卸载资源发起了 NDIS 状态指示，则必须按以下方式将[**ndis\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的成员设置为：

-   必须将**DestinationPortId**和**DestinationNicIndex**成员设置为分区所使用的网络连接的端口和网络适配器索引的相应值。

-   必须将**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**。

-   必须将**SourceNicIndex**成员设置为**NDIS\_交换机\_默认\_NIC\_索引**。

-   **StatusIndication**成员必须设置为指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。 此结构包含封装的 NDIS 状态指示的数据。

当扩展发出封装的 NDIS 状态指示时，必须执行以下步骤：

1.  该扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以便为源或目标网络适配器连接递增引用计数器。 这可以确保在其引用计数器为非零的情况下可扩展交换机接口将不会删除网络适配器连接。

    当扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)时，它将通过以下方式设置参数：

    -   如果转发扩展插件为基础物理适配器发起封装的 NDIS 状态指示，则会将*SwitchPortId*参数设置为为**SourcePortId**成员指定的值。 扩展还将*SwitchNicIndex*参数设置为为**SourceNicIndex**成员指定的值。

    -   如果为 Hyper-v 子分区发送了 NDIS 状态指示，则会将*SwitchPortId*参数设置为为**DestinationPortId**成员指定的值。 扩展还将*SwitchNicIndex*参数设置为为**DestinationNicIndex**成员指定的值。

    **请注意**  如果[*REFERENCESWITCHNIC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)未返回 NDIS\_STATUS\_SUCCESS，则无法发出封装的 NDIS 状态指示。

     

2.  该扩展调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)来转发封装的状态通知。

    **请注意**  如果扩展转发的是已筛选 OID 请求，则它必须在调用其[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数的上下文中调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 。

     

3.  [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)返回后，扩展将调用[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) ，以清除源或目标网络适配器连接的引用计数器。 该扩展将*SwitchPortId*和*SwitchNicIndex*参数设置为它在对[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的调用中使用的相同值。

 

 





