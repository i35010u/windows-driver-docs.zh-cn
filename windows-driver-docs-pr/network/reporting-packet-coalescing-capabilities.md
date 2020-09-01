---
title: 报告数据包合并功能
description: 报告数据包合并功能
ms.assetid: 6118F648-87FE-4B9E-9535-1602F4FF79D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cf7d4402c7e0f3450afacd662539007ba719711
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206247"
---
# <a name="reporting-packet-coalescing-capabilities"></a>报告数据包合并功能


小型端口驱动程序在网络适配器初始化期间向 NDIS 注册以下功能：

-   网络适配器支持的数据包合并功能。

-   当前在网络适配器上启用的数据包合并功能。

-   包合并会接收当前在网络适配器上启用的筛选功能。

**注意** 可以通过** \* PacketCoalescing** INF 关键字设置来启用或禁用对包合并的微型端口驱动程序支持。 此设置显示在网络适配器的 " **高级** " 属性页中。 有关 "数据包合并 INF 文件" 设置的详细信息，请参阅 [用于数据包合并的标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。



微型端口驱动程序通过 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构报告基础网络适配器的数据包合并和筛选功能。 如果注册表中的** \* PacketCoalescing**关键字设置的值为1，则启用数据包合并，并且微型端口驱动程序将按以下方式初始化**NDIS \_ 接收 \_ 筛选器 \_ 功能**结构：

1.  微型端口驱动程序初始化 **标头** 成员。 驱动程序将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。

    如果驱动程序支持数据包合并，则它会将**标头**的**修订**成员设置为 ndis \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2，并将**Size**成员设置为 ndis \_ SIZEOF \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2。

2.  微型端口驱动程序在 \_ \_ \_ \_ \_ \_ \_ \_ **SUPPORTEDQUEUEPROPERTIES** 成员中设置默认队列标志支持的 NDIS 接收筛选包合并。

    如果设置了此标志，网络适配器必须支持在硬件中筛选收到的多播数据包。 此筛选基于 NDIS 通过向网络适配器发送 [oid \_ 802 \_ 3 \_ 多播 \_ 列表](./oid-802-3-multicast-list.md) oid 集请求来将其卸载到网络适配器的多播地址。

    **注意**  协议驱动程序还可以通过发送 [OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](./oid-802-3-add-multicast-address.md) 和 [OID \_ 802 \_ 3 \_ DELETE \_ 多播 \_ address](./oid-802-3-delete-multicast-address.md) 请求，来更改多播地址列表的内容。 NDIS 将这些请求合并为 [oid \_ 802 \_ 3 \_ 多播 \_ 列表](./oid-802-3-multicast-list.md) oid 设置请求。




**注意**  适配器需要拒绝任何传入的多播数据包，其目标媒体访问控制 (MAC) 地址与这些 OID 集请求指定的任何多播地址都不匹配。




3.  微型端口驱动程序设置 \_ EnabledFilterTypes 成员中的 "NDIS 接收 \_ 筛选器 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" **EnabledFilterTypes**标志。

    **注意**  如果驱动程序设置此标志，则它还必须在 \_ \_ \_ \_ \_ \_ \_ \_ **SUPPORTEDQUEUEPROPERTIES** 成员中设置默认队列标志支持的 NDIS 接收筛选器数据包合并。 否则，NDIS 将通过返回 NDIS [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) \_ 状态 \_ 错误特性来对 NdisMSetMiniportAttributes 的调用失败 \_ 。



4.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须支持所有接收筛选器测试条件。 该驱动程序通过在 **SupportedFilterTests** 成员中设置以下标志来公布此支持：

    -   已 \_ 支持 NDIS 接收 \_ 筛选器 \_ 测试 \_ 标头 \_ 字段 \_ \_

    -   NDIS \_ 接收 \_ 筛选器 \_ 测试 \_ 标头 \_ 字段 \_ 掩码 \_ 等于 \_ 支持

    -   \_ \_ \_ \_ \_ \_ 不 \_ 等于 \_ 支持 NDIS 接收筛选器测试标头字段

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedFilterTests** 成员设置为零。



5.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则微型端口驱动程序必须支持在媒体访问控制的各个字段中筛选数据 (MAC) 、ip 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 标头。 该驱动程序通过在 **SupportedHeaders** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ MAC \_ 标头 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ ARP \_ 标头 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ IPV4 \_ 标头 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ IPV6 \_ 标头 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ UDP \_ 标头 \_

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedHeaders** 成员设置为零。



6.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，微型端口驱动程序必须支持在接收的数据包 (MAC) 标头的媒体访问控制中筛选数据。 该驱动程序通过在 **SupportedMacHeaderFields** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ MAC \_ 标头 \_ 目标 \_ 地址 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ MAC \_ 标头 \_ 协议 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ MAC \_ 标头 \_ 数据包 \_ 类型 \_

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedMacHeaderFields** 成员设置为零。



7.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，微型端口驱动程序必须支持在接收到的地址解析协议标头 (ARP) 数据包中筛选数据。 该驱动程序通过在 **SupportedARPHeaderFields** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ ARP \_ 标头 \_ 操作 \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ ARP \_ 标头 \_ SPA \_

    -   \_支持 NDIS 接收 \_ 筛选器 \_ ARP \_ 标头 \_ TPA \_

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedARPHeaderFields** 成员设置为零。



8.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则微型端口驱动程序必须支持在已接收 IP 版本 4 () 第 (3 层) 标头 (OSI 中筛选数据，) IPv4 数据包。 该驱动程序通过在 **SupportedIPv4HeaderFields** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ IPV4 \_ 标头 \_ 协议 \_

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedIPv4HeaderFields** 成员设置为零。



9.  如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，微型端口驱动程序必须支持在收到的 IP 版本 6 (IPv6) 数据包的 L3 标头中筛选数据。 该驱动程序通过在 **SupportedIPv6HeaderFields** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ IPV6 \_ 标头 \_ 协议 \_

    **注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedIPv6HeaderFields** 成员设置为零。



10. 如果微型端口驱动程序设置了 "NDIS \_ 接收 \_ 筛选器 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则微型端口驱动程序必须支持在 "接收的用户数据报协议" (L4) 标头中筛选数据， (UDP) 数据包。 该驱动程序通过在 **SupportedIUdpHeaderFields** 成员中设置以下标志来公布此支持：

    -   \_支持 NDIS 接收 \_ 筛选器 \_ UDP \_ 标头 \_ 目标 \_ 端口 \_

    **注意**  如果收到的 UDP 数据包包含 IPv4 选项或 IPv6 扩展标头，网络适配器可以处理该数据包，就好像它未通过 UDP 筛选器测试。 这样，适配器就可以自动删除已接收的数据包。




**注意**  如果微型端口驱动程序未设置 "NDIS \_ 接收 \_ 筛选 \_ 数据包 \_ 合并 \_ 筛选器 \_ 已启用" 标志，则驱动程序必须将 **SupportedIUdpHeaderFields** 成员设置为零。




11. 微型端口驱动程序必须报告可以为单个数据包合并筛选器指定的数据包标头字段上的最大测试数。 驱动程序在 **MaxFieldTestsPerPacketCoalescingFilter** 成员中指定此值。

    **注意**  支持数据包合并的网络适配器必须支持5个或更多可为单个数据包合并筛选器指定的数据包标头字段。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。



12. 微型端口驱动程序必须报告网络适配器所支持的数据包合并筛选器的最大数量。 驱动程序在 **MaxPacketCoalescingFilters** 成员中指定此值。

    **注意**  支持数据包合并的网络适配器必须支持10个或更多数据包合并筛选器。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。



当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序会按照以下步骤报告基础网络适配器的数据包合并和筛选功能：

-   微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构。

    如果注册表中的** \* PacketCoalescing**关键字设置的值为1，则微型端口驱动程序会将**HardwareReceiveFilterCapabilities**成员设置为指向先前初始化的[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。

    如果注册表中的** \* PacketCoalescing**关键字设置的值为零，则微型端口驱动程序不会播发对数据包合并的支持。 它必须将 **HardwareReceiveFilterCapabilities** 成员设置为 NULL。

-   驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

微型端口驱动程序用来报告基础网络适配器的数据包合并和筛选功能的方法基于用于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅 [报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。