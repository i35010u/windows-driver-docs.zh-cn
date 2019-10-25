---
title: 将 OID 请求转发到物理网络适配器
description: 将 OID 请求转发到物理网络适配器
ms.assetid: 2A6AA842-FFC2-4CEF-BA56-2FDB277E37C9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19826340aeacaeb7a8367f193684da70ced46f1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842127"
---
# <a name="forwarding-oid-requests-to-physical-network-adapters"></a>将 OID 请求转发到物理网络适配器


本主题讨论 Hyper-v 可扩展交换机扩展对底层物理适配器的对象标识符（OID）请求如何通过 Hyper-v 可扩展交换机控制路径。 扩展还可以按照本主题中所述的方法，将 OID 请求发送到基础物理网络适配器。

例如，可以将外部网络适配器绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。

在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 管理可扩展交换机团队的转发扩展称为*组合提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了 NDIS 6.40 （Windows Server 2012 R2）和更高版本的可扩展交换机团队的示例。

![ndis 6.40 的 oid 控制路径示意图](images/vswitch-oid-controlpath2-ndis640.png)

下图显示了 NDIS 6.30 （Windows Server 2012）的可扩展交换机团队示例。

![用于 ndis 6.30 的可扩展交换机团队示意图](images/vswitch-oid-controlpath2.png)

**请注意**，在 hyper-v 可扩展交换机接口中  ，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

必须封装 OID 请求，以将请求转发到基础物理网络适配器。 OID 请求首先封装在[**NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构内。 然后，OID 请求将通过 oid [\_switch\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)的 oid 集请求转发到可扩展交换机控制路径。

对底层物理适配器的 OID 请求由以下各项发出：

<a href="" id="the-extensible-switch-interface-"></a>可扩展交换机接口。  
OID 请求（如硬件卸载请求）由过量协议或筛选器驱动程序（在以下其中一种情况下运行）发出：

-   在 Hyper-v 父分区中运行的管理操作系统。

-   在 Hyper-v 子分区中运行的来宾操作系统。

当可扩展交换机接收到这些 OID 请求时，它们将封装在可扩展交换机控制路径上并进行转发。 当转发扩展插件收到封装的 OID 请求时，它可以将请求转发到基础物理适配器。 此功能对于为硬件卸载配置可扩展交换机团队特别有用。

例如，MUX 驱动程序会公布整个可扩展交换机团队的常见功能。 但是，转发扩展可以发出 OID 请求来查询或设置组内适配器的各个功能。 然后，转发扩展可从外部网络适配器发起 NDIS 状态指示，通知有关适用于整个团队的功能的过量驱动程序。 有关此过程的详细信息，请参阅[从物理网络适配器发起 NDIS 状态指示](originating-ndis-status-indications-from-physical-network-adapters.md)。

转发扩展在控制路径上转发 OID 请求时，由外部网络适配器接收。 此时，OID 请求是解封的，并转发到指定的物理网络适配器。

**注意**  从 Windows Server 2012 开始，将只封装硬件卸载 OID 请求并以这种方式转发这些请求。 例如，对虚拟机队列（VMQ）或 Internet 协议安全性（IPsec）的卸载 OID 请求被封装并转发到可扩展交换机控制路径。 有关详细信息，请参阅[管理对物理网络适配器的硬件卸载 OID 请求](managing-hardware-offload-oid-requests-to-physical-network-adapters.md)。

 

<a href="" id="a-forwarding-extension-"></a>转发扩展。  
转发扩展可以发起自己的封装 OID 请求，并将其转发到基础物理网络适配器。 转发扩展插件可以封装标准 NDIS OID 请求。 转发扩展还可以封装由独立硬件供应商（IHV）为物理网络适配器定义的专用 OID 请求。 这允许由 IHV 开发的转发扩展启用或禁用组中单个物理适配器上的专有属性。

此外，转发扩展插件还可以发起封装的硬件卸载 OID 请求，以为指定的 Hyper-v 子分区分配资源。 例如，转发扩展可以发起[\_接收\_筛选器的 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)的已封装 oid 请求\_分配\_队列，以便为指定的子分区分配 VMQ。 在这种情况下，该扩展会将请求封装为来自与分区关联的可扩展交换机端口和网络适配器连接。

**请  注意**，如果转发扩展正在筛选过量驱动程序发出的同一 OID 请求，则只能发起其自己的封装硬件卸载 OID 请求。 在这种情况下，扩展不能转发原始 OID 请求。 相反，该扩展插件必须调用[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete) ，以便在 NDIS 调用其[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)来完成发起的 OID 请求时完成此请求。

 

<a href="" id="filtering-or-capturing-extensions"></a>筛选或捕获扩展  
筛选或捕获扩展可以产生自己的封装 OID 查询请求，并将这些请求转发到基础物理网络适配器。 这些扩展插件可以封装由独立硬件供应商（IHV）为物理网络适配器定义的标准 NDIS OID 查询请求或专用 OID 查询请求。

**请注意**  仅转发扩展可将封装的 OID 集请求发起到基础物理适配器。

 

转发和重定向时，转发扩展必须遵循以下步骤，或发出基础物理适配器的封装 OID 请求：

1.  如果转发扩展插件是由 OID 请求引起的，则它必须使用与请求相关的信息来初始化扩展分配的[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。

    如果扩展插件转发 OID 请求，则不能更改[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数的*OidRequest*参数所引用的现有[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。 相反，扩展必须调用[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)为新的**ndis\_OID\_请求**结构分配内存，并复制现有**ndis\_OID\_请求**中的所有信息构造.

2.  该扩展将扩展分配的[**NDIS\_交换机\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的成员设置为以下值：

    -   **DestinationPortId**成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。

    -   **DestinationNicIndex**成员必须设置为底层物理网络适配器的非零索引值。

        有关这些索引值的详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

    -   如果转发扩展插件产生了对 Hyper-v 子分区的硬件卸载 OID 请求，则必须将**SourcePortId**成员设置为分区使用的端口的标识符。 此外， **SourceNicIndex**成员必须设置为到该端口的网络连接的网络适配器索引。

        如果转发扩展插件是根据其自身目的建立标准或专用 OID 请求，则必须将**SourcePortId**和**SourceNicIndex**成员设置为零。

        如果转发扩展转发或重定向硬件卸载 OID 请求，则必须保留由可扩展交换机接口设置的**SourcePortId**和**SourceNicIndex**成员的值。

    -   **OidRequest**成员必须设置为指向已初始化[**NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的指针\_封装的 OID 请求的请求结构。 转发扩展插件分配并初始化此结构，或使用结构的克隆副本。

3.  该扩展将扩展分配的[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的成员设置为以下值：

    -   **Oid**成员必须设置为[oid\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)。

    -   **InformationBuffer**成员必须包含指向缓冲区的指针，该缓冲区包含生成的或已筛选的 OID 请求数据。

    -   **InformationBufferLength**成员必须包含缓冲区的长度（以字节为单位），该缓冲区包含已生成或已筛选 OID 请求的数据。

    该扩展将其他成员设置为对[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构有效的值。

4.  扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)来递增目标物理网络适配器的索引的引用计数器。 这可确保在其引用计数器为非零的情况下，可扩展交换机接口将不会删除物理网络适配器连接。

    当扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)时，它会将*SwitchPortId*参数设置为为**DestinationPortId**成员指定的值。 扩展还将*SwitchNicIndex*参数设置为为**DestinationNicIndex**成员指定的值。

    **请注意**  如果[*REFERENCESWITCHNIC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)未返回 NDIS\_STATUS\_SUCCESS，则 OID 请求无法转发到目标物理网络适配器。

     

5.  如果转发扩展插件产生了对 Hyper-v 子分区的硬件卸载 OID 请求，它还会调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以便为与关联的源网络适配器连接的索引递增引用计数器依据. 这可确保在其引用计数器为非零的情况下，可扩展交换机接口将不会删除物理网络适配器连接。

    当扩展调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)时，它会将*SwitchPortId*参数设置为为**SourcePortId**成员指定的值。 扩展还将*SwitchNicIndex*参数设置为为**SourceNicIndex**成员指定的值。

    **请注意**  如果[*REFERENCESWITCHNIC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)未返回 NDIS\_STATUS\_SUCCESS，则 OID 请求无法转发到目标物理网络适配器。

     

6.  此扩展调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将封装的 OID 请求转发到指定的目标可扩展交换机端口和网络适配器。

    **请注意**  如果扩展转发的是已筛选 OID 请求，则它必须在调用其[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)函数的上下文中调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 。 如果该扩展插件已生成 OID 请求，则它会在正在*运行、正在* *重新启动*、*暂停*和*暂停*状态时调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 。 有关这些状态的详细信息，请参阅[筛选模块状态和操作](filter-module-states-and-operations.md)。

     

7.  当 NDIS 调用[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)函数时，扩展会调用[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) ，以清除目标物理网络适配器的索引的引用计数器。

    如果转发扩展插件产生了对 Hyper-v 子分区的硬件卸载 OID 请求，它还会调用[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来清除适配器的源网络适配器连接的索引引用计数器。

    在这两种情况下，扩展都将*SwitchPortId*和*SwitchNicIndex*参数设置为它在对[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的调用中使用的相同值。

有关扩展如何发出 OID 请求的详细信息，请参阅[从 NDIS 筛选器驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-filter-driver.md)。

有关 MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





