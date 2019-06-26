---
title: 确定接收筛选功能
description: 确定接收筛选功能
ms.assetid: 11EE5987-A2DE-4388-86D0-77285453E80A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d6b66d8ee3e5ffdc33f307a7a52e2964d6248e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381423"
---
# <a name="determining-receive-filtering-capabilities"></a>确定接收筛选功能


本主题介绍如何 NDIS 和基础驱动程序确定支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器的接收筛选功能。 本主题包含下列信息：

[报告接收过程的筛选功能*MiniportInitializeEx*](#reporting-receive-filtering-capabilities-during-miniportinitializeex)

[查询通过过量驱动程序接收的筛选功能](#querying-receive-filtering-capabilities-by-overlying-drivers)

**请注意**  只有微型端口驱动程序的可报告 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 网络适配器的接收筛选功能。 PCIe 虚函数 (VFs) 的微型端口驱动程序必须报告筛选功能的 SR-IOV 适配器的接收。

 

## <a name="reporting-receive-filtering-capabilities-during-miniportinitializeex"></a>报告接收过程的筛选功能*MiniportInitializeEx*


当 NDIS 调用 PF 微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，该驱动程序提供了以下接收筛选功能：

-   完整的硬件接收的网络适配器可以支持的筛选功能。

-   筛选功能的接口的当前启用的网络适配器上接收。

完整的硬件接收通过基础的网络适配器的筛选功能的微型端口驱动程序报告[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)按以下方式初始化结构：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

    从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_接收\_筛选器\_功能\_修订\_2，**大小**成员添加到 NDIS\_SIZEOF\_接收\_筛选器\_功能\_修订\_2。

2.  微型端口驱动程序设置的其他成员[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构与用于接收筛选的值的范围SR-IOV 网络适配器的功能。 例如，微型端口驱动程序设置相应标志**SupportedFilterTests**指定筛选器的微型端口驱动程序支持的测试操作。

3.  除了 SR-IOV，接收筛选中也使用了以下接口：

    -   [NDIS 数据包合并](ndis-packet-coalescing.md)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](managing-packet-coalescing-receive-filters.md)。

    -   [虚拟机队列 (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

    如果微型端口驱动程序支持以下任何接口，它还必须设置的成员[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构范围接收特定于该接口的筛选功能值。 例如，如果该驱动程序支持 NDIS 数据包合并和 SR-IOV，它必须设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_支持\_ON\_默认值\_中的队列标志**SupportedQueueProperties**成员。

微型端口驱动程序报告当前启用接收通过基础的网络适配器的筛选功能[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)按以下方式初始化结构：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

    从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_接收\_筛选器\_功能\_修订\_2，**大小**成员添加到 NDIS\_SIZEOF\_接收\_筛选器\_功能\_修订\_2。

2.  微型端口驱动程序设置的其他成员[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构与用于接收筛选的值的范围当前已启用的接口功能。 例如，如果启用了 NDIS 数据包合并，驱动程序必须仅设置特定于此技术的成员。

    启用或禁用通过标准化 INF 关键字的使用接收筛选的接口。 有关如何启用 NDIS 数据包合并的详细信息，请参阅[数据包合并标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。 有关如何启用 SR-IOV 和 VMQ 的详细信息，请参阅[处理 SR-IOV、 VMQ 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，该驱动程序注册接收筛选的网络适配器的功能，通过执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    微型端口驱动程序集**HardwareReceiveFilterCapabilities**成员添加到的地址[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 此结构是前面初始化完整的硬件接收的网络适配器的筛选功能。

2.  如果所有当前网络适配器上禁用 VMQ，SR-IOV 和 NDIS 数据包合并，微型端口驱动程序设置**CurrentReceiveFilterCapabilities**为 NULL 的成员。

3.  如果当前的网络适配器上已启用 VMQ、 SR-IOV 或 NDIS 数据包合并，微型端口驱动程序必须执行以下操作：

    -   微型端口驱动程序必须初始化另一个[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)与当前结构接收有关筛选功能网络适配器当前已启用接口。

        如果启用了 SR-IOV 接口，有些微型端口驱动程序必须在其中设置的成员的情况下[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的相同或不同的值。 这是因为 SR-IOV 接口提供类似的排队机制对 VMQ，但使用虚拟端口 (VPorts) 而不是 VM 接收队列。

        例如，微型端口驱动程序必须设置 NDIS\_接收\_筛选器\_VMQ\_筛选器\_中的已启用标志**EnabledFilterTypes**成员如果 VMQ 或启用 SR-IOV 接口。 但是，必须设置微型端口驱动程序**NumQueues**到零，如果启用 SR-IOV 接口和一个非零值，如果启用 VMQ 接口的成员。

    -   微型端口驱动程序集**CurrentReceiveFilterCapabilities**成员添加到的地址[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构，其中包含当前接收当前已启用接口的筛选功能。

4.  如果当前的网络适配器上已启用 VMQ、 SR-IOV 或 NDIS 数据包合并，微型端口驱动程序设置**HardwareReceiveFilterCapabilities**成员添加到的地址[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 此结构是使用之前初始化当前启用接收的网络适配器的筛选功能。

5.  驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-receive-filtering-capabilities-by-overlying-drivers"></a>查询通过过量驱动程序接收的筛选功能


网络适配器的当前启用的 NDIS 阶段接收到过量将绑定到如下所示的网络适配器的驱动程序的筛选功能：

-   当 NDIS 调用过量的筛选器驱动程序的[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数，NDIS 传递网络适配器的 NIC 交换机功能通过*AttachParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 **ReceiveFilterCapabilities**此结构的成员包含一个指向[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

-   当 NDIS 调用基础协议驱动[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数，NDIS 传递网络适配器的 NIC 交换机功能通过*BindParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 **ReceiveFilterCapabilities**此结构的成员包含一个指向[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

NDIS 也会返回[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构，当处理的对象标识符(OID)查询请求时[OID\_接收\_筛选器\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)并[OID\_接收\_筛选器\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)，颁发的过量协议或筛选器驱动程序。

 

 





