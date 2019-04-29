---
title: 将 OID 请求转发到物理网络适配器
description: 将 OID 请求转发到物理网络适配器
ms.assetid: 2A6AA842-FFC2-4CEF-BA56-2FDB277E37C9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b00e1b6ad41a5a10185ad0879468d4284164399
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356928"
---
# <a name="forwarding-oid-requests-to-physical-network-adapters"></a>将 OID 请求转发到物理网络适配器


本主题讨论如何 HYPER-V 可扩展交换机扩展将转发的基础上的 HYPER-V 可扩展交换机控制路径的物理适配器的对象标识符 (OID) 请求。 扩展还可以按照本主题中所述的方法源自对基础物理网络适配器的 OID 请求。

例如，外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。

在此配置中，向团队中每个网络适配器公开可扩展交换机扩展。 这允许要管理的配置和使用的团队中的单个网络适配器的扩展。 例如，转发扩展可用于负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 管理可扩展交换机团队的转发扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了一个可扩展交换机团队 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的示例。

![ndis 6.40 的 oid 控制路径的关系图](images/vswitch-oid-controlpath2-ndis640.png)

下图显示的 NDIS 6.30 (Windows Server 2012) 的可扩展交换机团队的示例。

![ndis 6.30 可扩展交换机团队的关系图](images/vswitch-oid-controlpath2.png)

**请注意**  中的 HYPER-V 可扩展交换机接口，NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*.

 

若要将请求转发到基础物理网络适配器都必须封装 OID 请求。 OID 请求首先封装在内[ **NDIS\_交换机\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构。 然后，OID 由 OID 集请求的请求通过可扩展交换机控制路径转发[OID\_切换\_NIC\_请求](https://msdn.microsoft.com/library/windows/hardware/hh598266)。

对基础物理适配器的 OID 请求颁发通过以下方法：

<a href="" id="the-extensible-switch-interface-"></a>可扩展交换机接口中。  
OID 请求，如将卸载对硬件的请求，颁发的过量协议或筛选器驱动程序运行在以下项之一：

-   管理操作系统的 HYPER-V 父分区中运行。

-   来宾操作系统运行的 HYPER-V 子分区中。

这些 OID 请求收到可扩展交换机，它们是封装，通过可扩展交换机控制路径转发。 转发扩展接收封装的 OID 请求时，它可以将请求转发到底层的物理适配器。 此功能是用于配置硬件卸载功能的可扩展交换机团队特别有用。

例如，MUX 驱动程序会通告整个可扩展交换机团队的常见功能。 但是，转发扩展可以发出 OID 请求查询或设置在团队中的适配器的各个功能。 然后，转发扩展可以源自 NDIS 状态指示从外部网络适配器，以通知有关将应用于整个团队的功能的基础驱动程序。 此过程的详细信息，请参阅[从物理网络适配器发起 NDIS 状态指示](originating-ndis-status-indications-from-physical-network-adapters.md)。

当转发扩展的控制路径通过将转发 OID 请求时，接收到外部网络适配器。 此时，OID 请求解封并转发到指定的物理网络适配器。

**请注意**  硬件卸载 OID 仅从 Windows Server 2012 中，请求是封装，并转发以这种方式。 例如，将卸载 OID 请求的虚拟机队列 (VMQ) 或 Internet 协议安全性 (IPsec) 是封装和通过可扩展交换机控制路径转发。 有关详细信息，请参阅[管理硬件卸载 OID 请求到物理网络适配器](managing-hardware-offload-oid-requests-to-physical-network-adapters.md)。

 

<a href="" id="a-forwarding-extension-"></a>转发扩展。  
转发扩展可以源自封装的 OID 请求并将其转发到基础物理网络适配器。 转发扩展可以封装标准 NDIS OID 请求。 转发扩展还可以封装由物理网络适配器的独立硬件供应商 (IHV) 定义的私有 OID 请求。 这允许由 IHV 可以启用或禁用在团队中的各个物理适配器的专有特性还开发一个转发扩展。

此外，转发扩展可以源自封装的硬件卸载 OID 请求为指定的 HYPER-V 子分区分配的资源。 例如，转发扩展可以源自的封装的 OID 请求[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)为指定子分配 VMQ分区。 在这种情况下，该扩展封装为来自与分区相关联的可扩展交换机端口和网络适配器连接请求。

**请注意**  转发扩展仅可以由自己封装的硬件卸载 OID 请求如果它正在筛选同一个 OID 请求已颁发的过量驱动程序。 在这种情况下，该扩展不能转发原始 OID 请求。 相反，扩展必须调用[ **NdisFOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561833)若要完成此请求时 NDIS 调用其[ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)若要完成起源于的 OID 请求。

 

<a href="" id="filtering-or-capturing-extensions"></a>筛选或捕获扩展  
筛选或捕获扩展可以源自其自身封装的 OID 查询请求并将其转发到基础物理网络适配器。 这些扩展可以封装标准 NDIS OID 查询请求或私有 OID 查询由物理网络适配器的独立硬件供应商 (IHV) 定义的请求。

**请注意**  仅转发扩展可以源自封装到基础物理适配器的 OID 集请求。

 

转发扩展转发，将重定向，或源自基础物理适配器的封装的 OID 请求时必须执行以下步骤：

1.  如果转发扩展原始的 OID 请求，它必须初始化扩展分配[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)与相关的信息的结构该请求。

    如果扩展转发 OID 请求，则必须更改现有[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构引用的*OidRequest*的参数[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)函数。 相反，扩展必须调用[ **NdisAllocateCloneOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff560706)若要为新分配内存**NDIS\_OID\_请求**结构和从现有复制所有信息**NDIS\_OID\_请求**结构。

2.  扩展设置的扩展插件分配成员[ **NDIS\_交换机\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构为以下值：

    -   **DestinationPortId**成员必须设置为外部网络适配器连接到可扩展的交换机端口的标识符。

    -   **DestinationNicIndex**成员必须设置为非零的索引值的基础物理网络适配器。

        有关这些索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

    -   如果转发扩展原始的 HYPER-V 子分区，硬件卸载 OID 请求**SourcePortId**成员必须设置为分区所使用的端口的标识符。 此外， **SourceNicIndex**成员必须设置为与该端口的网络连接的网络适配器的索引。

        如果转发扩展为自己的目的，原始的标准或专用 OID 请求**SourcePortId**并**SourceNicIndex**成员必须设置为零。

        如果转发扩展转发或重定向的硬件卸载 OID 请求，它必须保留的值**SourcePortId**并**SourceNicIndex**通过可扩展设置的成员交换机接口。

    -   **OidRequest**成员必须设置为指向一个已初始化的指针[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)封装 OID 请求的结构. 转发扩展分配和初始化此结构，或者使用该结构的克隆的副本。

3.  扩展设置的扩展插件分配成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构为以下值：

    -   **Oid**成员必须设置为[OID\_交换机\_NIC\_请求](https://msdn.microsoft.com/library/windows/hardware/hh598266)。

    -   **InformationBuffer**成员必须包含指向包含的生成或已筛选的 OID 请求数据的缓冲区的指针。

    -   **InformationBufferLength**成员必须包含包含生成或已筛选 OID 请求数据的缓冲区的长度，以字节为单位。

    扩展设置为有效的值的其他成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

4.  扩展调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增引用计数器，用于目标物理网络适配器的索引。 这可以保证可扩展交换机接口不会删除物理网络适配器连接时它的引用计数器为非零值。

    当扩展调用[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)，它会设置*SwitchPortId*参数指定的值**DestinationPortId**成员。 扩展还设置*SwitchNicIndex*为指定的值的参数**DestinationNicIndex**成员。

    **请注意**  如果[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)不会返回 NDIS\_状态\_成功后，OID 请求不能转发到目标物理网络适配器。

     

5.  如果转发扩展原始的 HYPER-V 子分区的硬件卸载 OID 请求，则还会调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增引用计数器，用于源的索引与分区相关联的网络适配器连接。 这可以保证可扩展交换机接口不会删除物理网络适配器连接时它的引用计数器为非零值。

    当扩展调用[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)，它会设置*SwitchPortId*参数指定的值**SourcePortId**成员。 扩展还设置*SwitchNicIndex*为指定的值的参数**SourceNicIndex**成员。

    **请注意**  如果[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)不会返回 NDIS\_状态\_成功后，OID 请求不能转发到目标物理网络适配器。

     

6.  扩展调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)封装的 OID 请求转发到指定的目标可扩展交换机端口和网络适配器。

    **请注意**  如果扩展转发经过筛选的 OID 请求，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)的调用上下文中其[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)函数。 如果扩展已生成的 OID 请求转发，则会调用[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)在时*运行*，*正在重新启动*，*已暂停*，和*暂停*状态。 有关这些状态的详细信息，请参阅[筛选器模块状态和操作](filter-module-states-and-operations.md)。

     

7.  当调用 NDIS [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)函数，扩展将调用[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)清除目标物理网络适配器的索引的引用计数器。

    如果转发扩展源于硬件卸载 OID 征求 HYPER-V 子分区，则还会调用[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)若要清除的源索引的引用计数器该适配器的网络适配器连接。

    在这两种情况下，扩展设置*SwitchPortId*并*SwitchNicIndex*相同的参数值对的调用中使用它[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294).

有关如何扩展发出 OID 请求的详细信息，请参阅[NDIS 筛选器驱动程序从生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





