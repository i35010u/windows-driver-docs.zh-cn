---
title: 从物理网络适配器转发 NDIS 状态指示
description: 从物理网络适配器转发 NDIS 状态指示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 538234fe3763c30497cda1a0829a532b81c29848
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792181"
---
# <a name="forwarding-ndis-status-indications-from-physical-network-adapters"></a>从物理网络适配器转发 NDIS 状态指示


本主题讨论可扩展交换机转发扩展使用的方法，以便从基础物理适配器转发 NDIS 状态指示。 一个或多个基础物理适配器可以绑定到 Hyper-v 可扩展交换机的外部网络适配器。

例如，可以将外部网络适配器绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。

在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 管理可扩展交换机团队的转发扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了来自 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的基础物理网络适配器中的 NDIS 状态指示的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.40 的物理网络适配器的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2-ndis640.png)

下图显示了 NDIS 6.30 (Windows Server 2012) 的基础物理网络适配器中的 NDIS 状态指示的 Hyper-v 可扩展交换机控制路径。

![用于 ndis 6.30 的物理网络适配器的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。

 

可扩展交换机接口转发由基础物理适配器生成的 NDIS 状态指示。 如果外部网络适配器绑定到可扩展交换机团队，则由 MUX 驱动程序的虚拟适配器边缘产生 NDIS 状态指示。 否则，状态指示由绑定到外部网络适配器的单个物理网络适配器发起。

当 NDIS 状态指示到达可扩展交换机接口时，它会将指示封装到 [**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构内。 然后，可扩展交换机的微型端口边缘发出包含此结构的 [**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 指示。

转发扩展收到 NDIS 状态指示后，它可以转发原始的指示数据或在转发指示之前修改数据。

**注意**  只有转发扩展才能在转发状态指示之前修改数据。 有关此类型的扩展的详细信息，请参阅 [转发扩展](forwarding-extensions.md)。

 

转发扩展可以从绑定到可扩展交换机外部网络适配器的任何基础物理适配器修改和转发状态指示。 通常，扩展会发出这些状态指示，以更改基础物理适配器的播发硬件卸载功能。 例如，扩展可以针对以下类型的硬件卸载修改和转发状态指示：

-   Internet 协议安全性 (IPsec)

-   虚拟机队列 (VMQ) 

-   单个根 i/o 虚拟化 (SR-IOV) 

如果转发扩展插件转发 NDIS 状态指示，则必须按以下方式设置 [**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构的成员：

-   **SourcePortId** 成员必须设置为外部网络适配器连接到的端口的标识符。 外部网络适配器绑定到一个或多个物理适配器。 有关详细信息，请参阅 [外部网络适配器](external-network-adapters.md)。

-   **SourceNicIndex** 成员必须设置为 NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX。 这允许将状态指示解释为来自绑定到外部网络适配器的整个可扩展交换机团队。

-   **DestinationPortId** 成员必须设置为 **NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。

-   **DestinationNicIndex** 成员必须设置为 **NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX**。

-   **StatusIndication** 成员必须设置为指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。 此结构包含封装的 NDIS 状态指示的数据。

当转发扩展发出封装的 NDIS 状态指示时，必须执行以下步骤：

1.  扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 来递增外部网络适配器的引用计数器。 这可以确保在其引用计数器为非零的情况下可扩展交换机接口将不会删除网络适配器连接。

    当扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)时，它会将 *SwitchPortId* 参数设置为为 **SourcePortId** 成员指定的值。 扩展还将 *SwitchNicIndex* 参数设置为为 **SourceNicIndex** 成员指定的值。

    **注意**  如果 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 未返回 NDIS \_ 状态 \_ 成功，则无法发出封装的 NDIS 状态指示。

     

2.  该扩展调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 来转发封装的状态通知。

    **注意** 如果扩展转发的是封装的 NDIS 状态指示，则必须在调用其 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数的上下文中调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 。

     

3.  [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)返回后，扩展将调用 [*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) ，以清除源或目标网络适配器连接的引用计数器。 该扩展将 *SwitchPortId* 和 *SwitchNicIndex* 参数设置为它在对 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的调用中使用的相同值。

有关 MUX 驱动程序的详细信息，请参阅 [NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

