---
title: 确定接收筛选功能
description: 确定接收筛选功能
ms.assetid: 11EE5987-A2DE-4388-86D0-77285453E80A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9811d1f9738bba889fc09f4bfe6bb01f4d1358da
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90812012"
---
# <a name="determining-receive-filtering-capabilities"></a>确定接收筛选功能


本主题介绍 NDIS 和过量驱动程序如何确定支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器接收筛选功能。 本主题包含以下信息：

[报告在*MiniportInitializeEx*期间接收筛选功能](#reporting-receive-filtering-capabilities-during-miniportinitializeex)

[查询过量驱动程序的接收筛选功能](#querying-receive-filtering-capabilities-by-overlying-drivers)

**注意**   仅适用于 SR-IOV 网络适配器的 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序可以报告接收筛选功能。 PCIe 虚拟功能 (VFs) 的微型端口驱动程序不能报告 SR-IOV 适配器的接收筛选功能。

 

## <a name="reporting-receive-filtering-capabilities-during-miniportinitializeex"></a>报告在*MiniportInitializeEx*期间接收筛选功能


当 NDIS 调用 PF 微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序提供以下接收筛选功能：

-   网络适配器可支持的完整硬件接收筛选功能。

-   当前在网络适配器上启用的接口的接收筛选功能。

微型端口驱动程序通过使用以下方法初始化的 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构来报告基础网络适配器的完整硬件接收筛选功能：

1.  微型端口驱动程序初始化 **标头** 成员。 驱动程序将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。

    从 NDIS 6.30 开始，微型端口驱动程序将**标头**的**修订**成员设置为 ndis \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2，并将**Size**成员设置为 ndis \_ SIZEOF \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2。

2.  微型端口驱动程序将 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的其他成员设置为 sr-iov 网络适配器接收筛选功能的值范围。 例如，微型端口驱动程序在 **SupportedFilterTests** 中设置相应的标志，以指定微型端口驱动程序支持的筛选器测试操作。

3.  除了 SR-IOV 外，接收筛选还用于以下接口：

    -   [NDIS 数据包合并](ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](guidelines-for-managing-packet-coalescing-receive-filters.md)。

    -   [虚拟机队列 (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

    如果微型端口驱动程序支持这些接口中的任何一个，则它还必须将 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的成员设置为特定于该接口的接收筛选功能值范围。 例如，如果驱动程序支持 NDIS 数据包合并和 SR-IOV，则必须在 \_ \_ \_ \_ \_ \_ \_ \_ **SUPPORTEDQUEUEPROPERTIES** 成员中设置默认队列标志支持的 ndis 接收筛选器数据包合并。

微型端口驱动程序通过使用以下方法初始化的 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构来报告当前启用的基础网络适配器接收筛选功能：

1.  微型端口驱动程序初始化 **标头** 成员。 驱动程序将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。

    从 NDIS 6.30 开始，微型端口驱动程序将**标头**的**修订**成员设置为 ndis \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2，并将**Size**成员设置为 ndis \_ SIZEOF \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2。

2.  微型端口驱动程序将 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的其他成员设置为当前启用的接口的接收筛选功能的值范围。 例如，如果启用了 NDIS 数据包合并，则驱动程序必须仅设置特定于此技术的成员。

    使用接收筛选的接口通过标准 INF 关键字启用或禁用。 有关如何启用 NDIS 数据包合并的详细信息，请参阅 [用于数据包合并的标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。 有关如何启用 SR-IOV 和 VMQ 的详细信息，请参阅 [处理 sr-iov、vmq 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序会按照以下步骤注册网络适配器的接收筛选功能：

1.  微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构。

    微型端口驱动程序将 **HardwareReceiveFilterCapabilities** 成员设置为 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的地址。 之前已通过网络适配器的完整硬件接收筛选功能对此结构进行了初始化。

2.  如果在网络适配器上当前禁用 VMQ、SR-IOV 和 NDIS 数据包合并，微型端口驱动程序会将 **CurrentReceiveFilterCapabilities** 成员设置为 NULL。

3.  如果当前在网络适配器上启用了 VMQ、SR-IOV 或 NDIS 数据包合并，则微型端口驱动程序必须执行以下操作：

    -   微型端口驱动程序必须用当前在网络适配器上启用的接口的当前接收筛选功能初始化另一个 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构。

        如果启用了 SR-IOV 接口，则在某些情况下，微型端口驱动程序必须将 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的成员设置为相同或不同的值。 这是因为 SR-IOV 接口向 VMQ 提供类似的排队机制，但使用 (VPorts) 的虚拟端口，而不是使用 VM 接收队列。

        例如，如果启用了 VMQ 或 SR-IOV 接口，微型端口驱动程序必须 \_ \_ 在 EnabledFilterTypes 成员中设置 NDIS 接收筛选器 \_ VMQ \_ 筛选器 \_ 已启用标志。 **EnabledFilterTypes** 但是，如果启用了 SR-IOV 接口，则微型端口驱动程序必须将 **NumQueues** 成员设置为零; 如果启用 VMQ 接口，则必须将其设置为非零值。

    -   微型端口驱动程序将 **CurrentReceiveFilterCapabilities** 成员设置为包含当前已启用接口的当前接收筛选功能的 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的地址。

4.  如果当前在网络适配器上启用了 VMQ、SR-IOV 或 NDIS 数据包合并，微型端口驱动程序会将 **HardwareReceiveFilterCapabilities** 成员设置为 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的地址。 之前已通过网络适配器的当前启用的接收筛选功能对此结构进行了初始化。

5.  驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

有关适配器初始化过程的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-receive-filtering-capabilities-by-overlying-drivers"></a>查询过量驱动程序的接收筛选功能


NDIS 通过以下方式将网络适配器的当前启用的接收筛选功能传递到绑定到网络适配器的过量驱动程序：

-   当 NDIS 调用过量筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数时，Ndis 通过 *AttachParameters* 参数传递网络适配器的 NIC 交换机功能。 此参数包含指向 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构的指针。 此结构的 **ReceiveFilterCapabilities** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的指针。

-   当 NDIS 调用过量协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数时，Ndis 通过 *BindParameters* 参数传递网络适配器的 NIC 交换机功能。 此参数包含指向 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构的指针。 此结构的 **ReceiveFilterCapabilities** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的指针。

NDIS 还会返回 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构，它处理的对象标识符 (Oid，) 查询请求 [oid \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md) ，以及由过量协议或筛选器驱动程序颁发的 [oid \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md) 。

 

