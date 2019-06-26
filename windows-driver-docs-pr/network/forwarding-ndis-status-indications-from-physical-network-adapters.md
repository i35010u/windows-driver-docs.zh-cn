---
title: 从物理网络适配器转发 NDIS 状态指示
description: 从物理网络适配器转发 NDIS 状态指示
ms.assetid: 6EE9BB96-FFAB-4844-9F74-43FB3F18FAB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcebb16461d63e52b4be8a510266f9f910e1aca3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353339"
---
# <a name="forwarding-ndis-status-indications-from-physical-network-adapters"></a>从物理网络适配器转发 NDIS 状态指示


本主题讨论从基础物理适配器到正向 NDIS 状态指示转发扩展的可扩展交换机使用的方法。 一个或多个基础物理适配器可以绑定到外部网络适配器的 HYPER-V 可扩展交换机。

例如，外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。

在此配置中，向团队中每个网络适配器公开可扩展交换机扩展。 这允许要管理的配置和使用的团队中的单个网络适配器的扩展。 例如，转发扩展可用于负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 管理可扩展交换机团队的转发扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

下图显示从 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的基础物理网络适配器的 NDIS 状态指示的 HYPER-V 可扩展交换机控制路径。

![从物理网络适配器的 ndis 6.40 ndis 状态指示 vswitch 控制路径](images/vswitch-status-controlpath2-ndis640.png)

下图显示 NDIS 状态指示的 HYPER-V 可扩展交换机控制路径从基础物理网络适配器的 NDIS 6.30 (Windows Server 2012)。

![从物理网络适配器的 ndis 6.30 ndis 状态指示 vswitch 控制路径](images/vswitch-status-controlpath2.png)

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*.

 

可扩展交换机接口将转发所带来的基础物理适配器的 NDIS 状态指示。 如果外部网络适配器绑定到可扩展交换机团队，MUX 驱动程序的虚拟适配器边缘源于 NDIS 状态指示。 否则，状态指示发出由单一物理网络适配器绑定到外部网络适配器。

当在可扩展交换机接口到达 NDIS 状态指示时，它封装在指示[ **NDIS\_切换\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。 然后，可扩展交换机问题的微型端口边缘[ **NDIS\_状态\_切换\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示包含此结构。

一旦转发扩展收到 NDIS 状态指示，可以将原始指示数据转发或修改数据，然后它会指示转发。

**请注意**  仅转发扩展转发的状态指示之前可以修改的数据。 有关此类型的扩展的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

 

转发扩展可以修改和转发状态指示来自任何基础物理适配器的绑定到可扩展交换机的外部网络适配器。 通常情况下，该扩展会发出这些状态指示更改播发的硬件卸载功能的基础物理适配器。 例如，扩展可以修改和转发以下类型的硬件卸载功能的状态指示：

-   Internet 协议安全 (IPsec)

-   虚拟的机队列 (VMQ)

-   单根 I/O 虚拟化 (SR-IOV)

如果转发扩展转发的 NDIS 状态指示，它必须设置的成员[ **NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构如下所示：

-   **SourcePortId**成员必须设置为外部网络适配器连接到的端口的标识符。 外部网络适配器绑定到一个或多个物理适配器。 有关详细信息，请参阅[外部的网络适配器](external-network-adapters.md)。

-   **SourceNicIndex**成员必须设置为 NDIS\_交换机\_默认\_NIC\_索引。 这允许将被解释为源自于的整个可扩展交换机团队的绑定到外部网络适配器的状态指示。

-   **DestinationPortId**成员必须设置为**NDIS\_交换机\_默认\_端口\_ID**。

-   **DestinationNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**。

-   **StatusIndication**成员必须设置为指向的指针[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。 此结构包含封装的 NDIS 状态指示的数据。

当转发扩展问题时封装的 NDIS 状态指示时，它必须执行以下步骤：

1.  扩展调用[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)递增引用计数器，用于外部网络适配器。 这可以保证可扩展交换机接口不会删除网络适配器连接时它的引用计数器为非零值。

    当扩展调用[ *ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)，它会设置*SwitchPortId*参数指定的值**SourcePortId**成员。 扩展还设置*SwitchNicIndex*为指定的值的参数**SourceNicIndex**成员。

    **请注意**  如果[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)不会返回 NDIS\_状态\_成功后，无法发出封装的 NDIS 状态指示.

     

2.  扩展调用[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)转发封装的状态通知。

    **请注意**  如果扩展转发封装的 NDIS 状态指示，它必须调用[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)其调用的上下文中[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数。

     

3.  之后[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)返回时，扩展调用[ *DereferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)若要清除的引用计数器源或目标网络适配器连接。 扩展集*SwitchPortId*并*SwitchNicIndex*相同的参数值对的调用中使用它[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic).

MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





