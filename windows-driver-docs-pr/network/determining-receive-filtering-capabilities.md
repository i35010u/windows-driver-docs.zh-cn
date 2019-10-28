---
title: 确定接收筛选功能
description: 确定接收筛选功能
ms.assetid: 11EE5987-A2DE-4388-86D0-77285453E80A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba9ee2381a71c34cfb91a5ed34deac818c31033e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838143"
---
# <a name="determining-receive-filtering-capabilities"></a>确定接收筛选功能


本主题介绍 NDIS 和过量驱动程序如何确定支持单个根 i/o 虚拟化（SR-IOV）的网络适配器的接收筛选功能。 本主题包含下列信息：

[报告在*MiniportInitializeEx*期间接收筛选功能](#reporting-receive-filtering-capabilities-during-miniportinitializeex)

[查询过量驱动程序的接收筛选功能](#querying-receive-filtering-capabilities-by-overlying-drivers)

**请注意**  仅适用于 sr-iov 网络适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序可以报告接收筛选功能。 PCIe 虚拟功能（VFs）的微型端口驱动程序不能报告 SR-IOV 适配器的接收筛选功能。

 

## <a name="reporting-receive-filtering-capabilities-during-miniportinitializeex"></a>报告在*MiniportInitializeEx*期间接收筛选功能


当 NDIS 调用 PF 微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序提供以下接收筛选功能：

-   网络适配器可支持的完整硬件接收筛选功能。

-   当前在网络适配器上启用的接口的接收筛选功能。

微型端口驱动程序通过[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构，通过以下方式来报告基础网络适配器的完整硬件接收筛选功能：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

    从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 ndis\_接收\_筛选器\_功能\_修订版本\_2，并将**Size**成员设置为 ndis\_SIZEOF\_接收\_筛选器\_功能\_修订版本\_2。

2.  微型端口驱动程序将[**NDIS\_接收\_筛选\_器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的其他成员设置为 sr-iov 网络适配器接收筛选功能的值范围。 例如，微型端口驱动程序在**SupportedFilterTests**中设置相应的标志，以指定微型端口驱动程序支持的筛选器测试操作。

3.  除了 SR-IOV 外，接收筛选还用于以下接口：

    -   [NDIS 数据包合并](ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](managing-packet-coalescing-receive-filters.md)。

    -   [虚拟机队列 (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

    如果微型端口驱动程序支持这些接口中的任何一个，则它还必须将[**NDIS\_接收\_筛选\_器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的成员设置为特定于该接口的接收筛选功能值范围。 例如，如果驱动程序支持 NDIS 数据包合并和 SR-IOV，则必须将 NDIS\_接收\_筛选器\_数据包\_合并\_\_默认\_队列标志**SupportedQueueProperties**成员。

微型端口驱动程序通过[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构，通过以下方式来报告当前启用的基础网络适配器的接收筛选功能：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

    从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 ndis\_接收\_筛选器\_功能\_修订版本\_2，并将**Size**成员设置为 ndis\_SIZEOF\_接收\_筛选器\_功能\_修订版本\_2。

2.  微型端口驱动程序将[**NDIS\_接收\_\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的其他成员设置为已启用的接口的接收筛选功能的值范围。 例如，如果启用了 NDIS 数据包合并，则驱动程序必须仅设置特定于此技术的成员。

    使用接收筛选的接口通过标准 INF 关键字启用或禁用。 有关如何启用 NDIS 数据包合并的详细信息，请参阅[用于数据包合并的标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。 有关如何启用 SR-IOV 和 VMQ 的详细信息，请参阅[处理 sr-iov、vmq 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序会按照以下步骤注册网络适配器的接收筛选功能：

1.  微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    微型端口驱动程序将**HardwareReceiveFilterCapabilities**成员设置为[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的地址。 之前已通过网络适配器的完整硬件接收筛选功能对此结构进行了初始化。

2.  如果在网络适配器上当前禁用 VMQ、SR-IOV 和 NDIS 数据包合并，微型端口驱动程序会将**CurrentReceiveFilterCapabilities**成员设置为 NULL。

3.  如果当前在网络适配器上启用了 VMQ、SR-IOV 或 NDIS 数据包合并，则微型端口驱动程序必须执行以下操作：

    -   微型端口驱动程序必须将另一个[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构与当前在网络适配器上启用的接口的当前接收筛选功能结合在一起。

        如果启用了 SR-IOV 接口，则在某些情况下，微型端口驱动程序必须将[**NDIS\_接收\_筛选\_器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的成员设置为相同或不同的值。 这是因为 SR-IOV 接口向 VMQ 提供类似的排队机制，但使用虚拟端口（VPorts）而不是 VM 接收队列。

        例如，如果启用了 VMQ 或 SR-IOV 接口，微型端口驱动程序必须在**EnabledFilterTypes**成员中设置 NDIS\_接收\_FILTER\_VMQ\_筛选器\_启用标志。 但是，如果启用了 SR-IOV 接口，则微型端口驱动程序必须将**NumQueues**成员设置为零; 如果启用 VMQ 接口，则必须将其设置为非零值。

    -   微型端口驱动程序将**CurrentReceiveFilterCapabilities**成员设置为[**NDIS\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的地址，\_功能结构包含的当前接收筛选功能当前支持的接口。

4.  如果当前在网络适配器上启用了 VMQ、SR-IOV 或 NDIS 数据包合并，微型端口驱动程序会将**HardwareReceiveFilterCapabilities**成员设置为[**NDIS\_接收\_筛选器的地址\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 之前已通过网络适配器的当前启用的接收筛选功能对此结构进行了初始化。

5.  驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-receive-filtering-capabilities-by-overlying-drivers"></a>查询过量驱动程序的接收筛选功能


NDIS 通过以下方式将网络适配器的当前启用的接收筛选功能传递到绑定到网络适配器的过量驱动程序：

-   当 NDIS 调用过量筛选器驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数时，Ndis 通过*AttachParameters*参数传递网络适配器的 NIC 交换机功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**ReceiveFilterCapabilities**成员包含指向[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。

-   当 NDIS 调用过量协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 通过*BindParameters*参数传递网络适配器的 NIC 交换机功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**ReceiveFilterCapabilities**成员包含指向[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。

在处理 OID 的对象标识符（OID）查询请求时，NDIS 还[**会返回 ndis\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构[\_接收\_筛选器\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)和OID\_接收由过量协议或筛选器驱动程序颁发[\_硬件\_功能\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)。

 

 





