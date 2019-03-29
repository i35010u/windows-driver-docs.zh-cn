---
title: 发起从物理网络适配器的 NDIS 状态指示
description: 从物理网络适配器发起 NDIS 状态指示
ms.assetid: D588CD7E-98A3-4BA8-A467-6492DA2186CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9261ff1785e113957e549d2028a5ba17651d633
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567671"
---
# <a name="originating-ndis-status-indications-from-physical-network-adapters"></a>从物理网络适配器发起 NDIS 状态指示


本主题讨论由转发扩展的可扩展交换机打出连接到交换机的网络适配器的 NDIS 状态指示的方法。 该扩展可以源自 NDIS 状态指示对于以下类型的适配器：

-   一个或多个基础绑定到的物理适配器[外部网络适配器](external-network-adapters.md)的可扩展交换机。

    例如，外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。

    在此配置中，向团队中每个网络适配器公开可扩展交换机扩展。 这允许要管理的配置和使用的团队中的单个网络适配器的扩展。 例如，转发扩展可用于负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 管理可扩展交换机团队的转发扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

-   虚拟机 (VM) 网络适配器的 HYPER-V 子分区中公开并连接到可扩展交换机端口。

下图显示了有关 NDIS 状态指示从物理和虚拟机网络适配器的 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的 HYPER-V 可扩展交换机控制路径。

![有关从 ndis 6.40 及更高版本的物理和虚拟机网络适配器的 ndis 状态指示 vswitch 控制路径](images/vswitch-status-controlpath3-ndis640.png)

下图显示了从物理 NDIS 状态指示的 HYPER-V 可扩展交换机控制路径和 VM 网络适配器的 NDIS 6.30 (Windows Server 2012)。

![ndis 状态指示从物理和虚拟机网络适配器的 ndis 6.30 的 vswitch 控制路径](images/vswitch-status-controlpath3.png)

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

转发扩展可以源自封装的硬件卸载状态指示为过量可扩展交换机驱动程序堆栈中的驱动程序。 这也允许扩展来更改绑定到外部网络适配器的可扩展交换机的物理适配器的基础团队的当前卸载功能。 团队的适配器绑定到外部网络适配器，仅在团队的常见功能会播发到 NDIS 或基础协议和筛选器驱动程序。 该扩展可以通过发起封装的状态指示要播发由团队中的某些适配器支持的功能扩展的播发的功能。 例如，扩展可以发出封装[ **NDIS\_状态\_接收\_筛选器\_当前\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh439814)表示要更改当前已启用接收整个团队的筛选器功能。

**请注意**  仅转发扩展可以源自封装的状态指示。 有关此类型的扩展的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

 

通常情况下，转发扩展之后，封装的 NDIS 状态指示，若要更改播发的硬件卸载功能的基础物理适配器。 例如，扩展可以源自以下类型的硬件卸载功能的状态指示：

-   Internet 协议安全 (IPsec)。

-   虚拟的机队列 (VMQ)。

-   单根 I/O 虚拟化 (SR-IOV)。

转发扩展还可以源自封装的 NDIS 状态指示，若要更改为 HYPER-V 子分区分配的硬件卸载资源。 从 NDIS 6.30 开始，扩展可以发出封装[ **NDIS\_状态\_交换机\_端口\_删除\_VF** ](https://msdn.microsoft.com/library/windows/hardware/hh598206)表示要删除的 VM 网络适配器和 PCI Express (PCIe) 的虚拟函数 (VF) 之间的绑定。 公开和受支持的基础物理网络适配器 VF[单个根 I/O 虚拟化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)接口。

如果转发扩展源自封装的 NDIS 状态硬件卸载资源的指示基础物理适配器，它必须设置的成员[ **NDIS\_交换机\_NIC\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/hh598217)结构如下所示：

-   **DestinationPortId**成员必须设置为**NDIS\_交换机\_默认\_端口\_ID**。
-   **DestinationNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**

-   **SourcePortId**成员必须设置为外部网络适配器连接到可扩展的交换机端口的标识符。

-   **SourceNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**。 这允许将被解释为源自于的整个可扩展交换机团队的绑定到外部网络适配器的状态指示。

    **请注意**  转发扩展还必须将此成员设置为**NDIS\_交换机\_默认\_NIC\_索引**如果单个物理网络适配器是绑定到外部网络适配器。

     

-   **StatusIndication**成员必须设置为指向的指针[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 此结构包含封装的 NDIS 状态指示的数据。

如果转发扩展原始 NDIS 状态硬件卸载资源的指示 HYPER-V 子分区，则必须设置的成员[ **NDIS\_交换机\_NIC\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/hh598217)结构如下所示：

-   **DestinationPortId**并**DestinationNicIndex**成员必须设置为分区所使用的网络连接的端口和网络适配器索引的相应值。

-   **SourcePortId**成员必须设置为**NDIS\_交换机\_默认\_端口\_ID**。

-   **SourceNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**。

-   **StatusIndication**成员必须设置为指向的指针[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 此结构包含封装的 NDIS 状态指示的数据。

当扩展问题时封装的 NDIS 状态指示时，它必须执行以下步骤：

1.  扩展调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增引用计数器，用于源或目标网络适配器连接。 这可以保证可扩展交换机接口不会删除网络适配器连接时它的引用计数器为非零值。

    当扩展调用[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)，它按以下方式设置的参数：

    -   如果转发扩展原始封装的 NDIS 状态指示为基础的物理适配器，它会设置*SwitchPortId*为指定的值的参数**SourcePortId**成员。 扩展还设置*SwitchNicIndex*为指定的值的参数**SourceNicIndex**成员。

    -   如果转发扩展原始的 HYPER-V 子分区 NDIS 状态指示，它会设置*SwitchPortId*为指定的值的参数**DestinationPortId**成员。 扩展还设置*SwitchNicIndex*为指定的值的参数**DestinationNicIndex**成员。

    **请注意**  如果[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)不会返回 NDIS\_状态\_成功后，无法发出封装的 NDIS 状态指示.

     

2.  扩展调用[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)转发封装的状态通知。

    **请注意**  如果扩展转发经过筛选的 OID 请求，它必须调用[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)的调用上下文中其[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)函数。

     

3.  之后[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)返回时，扩展调用[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)若要清除的引用计数器源或目标网络适配器连接。 扩展集*SwitchPortId*并*SwitchNicIndex*相同的参数值对的调用中使用它[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294).

 

 





