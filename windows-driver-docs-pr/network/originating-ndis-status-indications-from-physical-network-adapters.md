---
title: 从物理网络适配器发起 NDIS 状态指示
description: 从物理网络适配器发起 NDIS 状态指示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de1a9b7afcc62cdbb30037f834a8ef650bb5271e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832133"
---
# <a name="originating-ndis-status-indications-from-physical-network-adapters"></a>从物理网络适配器发起 NDIS 状态指示


本主题讨论可扩展交换机转发扩展插件为连接到交换机的网络适配器发起 NDIS 状态指示所使用的方法。 扩展可以针对以下类型的适配器发起 NDIS 状态指示：

-   绑定到可扩展交换机的 [外部网络适配器](external-network-adapters.md) 的一个或多个基础物理适配器。

    例如，可以将外部网络适配器绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。

    在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 管理可扩展交换机团队的转发扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

-   虚拟机 (VM) 网络适配器，该适配器在 Hyper-v 子分区内公开并连接到可扩展交换机端口。

下图显示了适用于 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的物理和 VM 网络适配器中的 NDIS 状态指示的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.40 和更高版本的物理和 vm 网络适配器中的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath3-ndis640.png)

下图显示了适用于 NDIS 6.30 (Windows Server 2012) 的物理和 VM 网络适配器的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.30 的物理和 vm 网络适配器的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath3.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。

 

转发扩展可将封装的硬件卸载状态指示发送到可扩展交换机驱动程序堆栈中的过量驱动程序。 这也允许该扩展插件更改绑定到可扩展交换机外部网络适配器的物理适配器的底层团队的当前卸载功能。 当适配器组绑定到外部网络适配器时，仅将团队的常见功能播发到 NDIS 或过量的协议和筛选器驱动程序。 扩展可以通过将封装的状态指示起源到团队中某些适配器支持的播发功能来扩展播发功能。 例如，扩展可以发出封装的 [**NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 当前 \_ 功能**](./ndis-status-receive-filter-current-capabilities.md) 指示来更改整个团队的当前启用的接收筛选器功能。

**注意**  只有转发扩展可以产生封装的状态指示。 有关此类型的扩展的详细信息，请参阅 [转发扩展](forwarding-extensions.md)。

 

通常情况下，转发扩展会产生封装的 NDIS 状态指示，以更改基础物理适配器的播发硬件卸载功能。 例如，扩展可能会产生以下类型的硬件卸载的状态指示：

-   Internet 协议安全 (IPsec) 。

-   虚拟机队列 (VMQ) 。

-   单根 I/O 虚拟化 (SR-IOV)。

转发扩展还可以发起封装的 NDIS 状态指示，以更改为 Hyper-v 子分区分配的硬件卸载资源。 从 NDIS 6.30 开始，扩展可以发出封装的 [**NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF**](./ndis-status-switch-port-remove-vf.md) 指示，以删除 VM 网络适配器与 PCI Express (PCIe 之间的绑定) 虚函数 (VF) 。 VF 由支持 [单个根 i/o 虚拟化 ](single-root-i-o-virtualization--sr-iov-.md) 的基础物理网络适配器公开和支持 (sr-iov) 接口。

如果转发扩展插件为基础物理适配器的硬件卸载资源产生了一个封装的 NDIS 状态指示，则必须按以下方式设置 [**NDIS \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构的成员：

-   **DestinationPortId** 成员必须设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。
-   **DestinationNicIndex** 成员必须设置为 **NDIS \_ 交换机 \_ 默认 \_ NIC \_ 索引**

-   **SourcePortId** 成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。

-   **SourceNicIndex** 成员必须设置为 **NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX**。 这允许将状态指示解释为来自绑定到外部网络适配器的整个可扩展交换机团队。

    **注意**  如果只有一个物理网络适配器绑定到外部网络适配器，则转发扩展还必须将此成员设置为 **NDIS \_ 交换机 \_ 默认 \_ NIC \_ 索引** 。

     

-   **StatusIndication** 成员必须设置为指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。 此结构包含封装的 NDIS 状态指示的数据。

如果转发扩展插件为 Hyper-v 子分区的硬件卸载资源发起了 NDIS 状态指示，则必须按以下方式设置 [**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构的成员：

-   必须将 **DestinationPortId** 和 **DestinationNicIndex** 成员设置为分区所使用的网络连接的端口和网络适配器索引的相应值。

-   **SourcePortId** 成员必须设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。

-   **SourceNicIndex** 成员必须设置为 **NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX**。

-   **StatusIndication** 成员必须设置为指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。 此结构包含封装的 NDIS 状态指示的数据。

当扩展发出封装的 NDIS 状态指示时，必须执行以下步骤：

1.  该扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以便为源或目标网络适配器连接递增引用计数器。 这可以确保在其引用计数器为非零的情况下可扩展交换机接口将不会删除网络适配器连接。

    当扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)时，它将通过以下方式设置参数：

    -   如果转发扩展插件为基础物理适配器发起封装的 NDIS 状态指示，则会将 *SwitchPortId* 参数设置为为 **SourcePortId** 成员指定的值。 扩展还将 *SwitchNicIndex* 参数设置为为 **SourceNicIndex** 成员指定的值。

    -   如果为 Hyper-v 子分区发送了 NDIS 状态指示，则会将 *SwitchPortId* 参数设置为为 **DestinationPortId** 成员指定的值。 扩展还将 *SwitchNicIndex* 参数设置为为 **DestinationNicIndex** 成员指定的值。

    **注意**  如果 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 未返回 NDIS \_ 状态 \_ 成功，则无法发出封装的 NDIS 状态指示。

     

2.  该扩展调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 来转发封装的状态通知。

    **注意** 如果扩展转发的是已筛选 OID 请求，则必须在调用其 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数的上下文中调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 。

     

3.  [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)返回后，扩展将调用 [*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) ，以清除源或目标网络适配器连接的引用计数器。 该扩展将 *SwitchPortId* 和 *SwitchNicIndex* 参数设置为它在对 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的调用中使用的相同值。

 

