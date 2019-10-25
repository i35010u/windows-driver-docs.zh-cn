---
title: 报告数据包合并功能
description: 报告数据包合并功能
ms.assetid: 6118F648-87FE-4B9E-9535-1602F4FF79D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6cf6184fe6467341f9f2e99605b44cb685f8fa6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842042"
---
# <a name="reporting-packet-coalescing-capabilities"></a>报告数据包合并功能


小型端口驱动程序在网络适配器初始化期间向 NDIS 注册以下功能：

-   网络适配器支持的数据包合并功能。

-   当前在网络适配器上启用的数据包合并功能。

-   包合并会接收当前在网络适配器上启用的筛选功能。

**注意** 可以通过 **\*PacketCoalescing** INF 关键字 "设置启用或禁用对包合并的微型端口驱动程序支持。 此设置显示在网络适配器的 "**高级**" 属性页中。 有关 "数据包合并 INF 文件" 设置的详细信息，请参阅[用于数据包合并的标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。



微型端口驱动程序通过[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构来报告基础网络适配器的数据包合并和筛选功能。 如果注册表中的 **\*PacketCoalescing**关键字设置的值为1，则启用数据包合并，而微型端口驱动程序将初始化**NDIS\_接收\_筛选\_器**如下所示：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

    如果驱动程序支持数据包合并，则它会将**标头**的**修订**成员设置为 ndis\_接收\_筛选器\_功能\_修订\_2，并将**Size**成员设置为 ndis\_SIZEOF\_接收\_筛选\_功能\_修订版本\_2。

2.  微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_在**SupportedQueueProperties**成员的\_默认\_QUEUE 标志上\_支持的合并。

    如果设置了此标志，网络适配器必须支持在硬件中筛选收到的多播数据包。 此筛选基于 NDIS 卸载到网络适配器的多播地址， [\_802\_3\_多播\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)OID 设置请求。

    **注意** 协议驱动程序还可以通过发送 OID 来更改多播地址列表的内容， [\_802\_3\_添加\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)和[OID\_802\_3\_删除\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)请求。 NDIS 将这些请求合并到[oid\_802\_3\_多播\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)OID 设置请求。




**注意** 适配器需要拒绝任何传入的多播数据包，其目标媒体访问控制（MAC）地址与这些 OID 集请求指定的任何多播地址都不匹配。




3.  微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_在**EnabledFilterTypes**成员中启用标志。

    **注意** 如果驱动程序设置此标志，则它还必须将 NDIS\_接收\_筛选器\_数据包\_合并，\_在**SupportedQueueProperties**成员中\_默认\_QUEUE 标志。 否则，NDIS 会通过返回 NDIS\_状态\_错误\_特性来对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用失败。



4.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须支持所有接收筛选器测试条件。 该驱动程序通过在**SupportedFilterTests**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_测试\_标头\_字段\_支持相等\_

    -   NDIS\_接收\_筛选器\_测试\_标头\_\_\_

    -   NDIS\_接收\_筛选器\_测试\_标头\_字段\_不支持\_相等\_

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedFilterTests**成员设置为零。



5.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则微型端口驱动程序必须支持在媒体访问控制（MAC）的各个字段内筛选数据、IP 版本4（IPv4）和 IP 版本6（IPv6）标头。 该驱动程序通过在**SupportedHeaders**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_MAC\_标头\_支持

    -   NDIS\_接收\_筛选器\_ARP\_标头\_支持

    -   NDIS\_接收\_筛选器\_IPV4\_标头\_支持

    -   NDIS\_接收\_筛选器\_IPV6\_标头\_支持

    -   NDIS\_接收\_筛选器\_UDP\_标头\_支持

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedHeaders**成员设置为零。



6.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_启用标志\_筛选器，则微型端口驱动程序必须支持对接收的数据包。 该驱动程序通过在**SupportedMacHeaderFields**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_MAC\_标头\_目标\_支持的地址\_

    -   NDIS\_接收\_筛选器\_MAC\_标头\_协议\_支持

    -   NDIS\_接收\_筛选器\_MAC\_标头\_支持数据包\_类型\_

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedMacHeaderFields**成员设置为零。



7.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则微型端口驱动程序必须支持在收到的地址解析标头内筛选数据协议（ARP）数据包。 该驱动程序通过在**SupportedARPHeaderFields**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_ARP\_标头\_操作\_支持

    -   NDIS\_接收\_筛选器\_ARP\_标头\_支持 SPA\_

    -   NDIS\_接收\_筛选器\_ARP\_标头\_支持的\_TPA

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedARPHeaderFields**成员设置为零。



8.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则微型端口驱动程序必须支持在开放系统互连（OSI）第3层中筛选数据（L3）标头，接收的 IP 版本4（IPv4）数据包。 该驱动程序通过在**SupportedIPv4HeaderFields**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_IPV4\_标头\_协议\_受支持

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedIPv4HeaderFields**成员设置为零。



9.  如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_启用标志\_筛选器，则微型端口驱动程序必须支持在收到的 IP 版本6（IPv6）的 L3 标头内筛选数据数据包. 该驱动程序通过在**SupportedIPv6HeaderFields**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_IPV6\_标头\_协议\_支持

    **注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedIPv6HeaderFields**成员设置为零。



10. 如果微型端口驱动程序将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则微型端口驱动程序必须支持对已接收用户的 OSI 第4（L4）标头中的数据进行筛选数据报协议（UDP）数据包。 该驱动程序通过在**SupportedIUdpHeaderFields**成员中设置以下标志来公布此支持：

    -   NDIS\_接收\_筛选器\_UDP\_标头\_目标\_支持的端口\_

    **注意** 如果收到的 UDP 数据包包含 IPv4 选项或 IPv6 扩展标头，网络适配器可以处理该数据包，就好像它未通过 UDP 筛选器测试。 这样，适配器就可以自动删除已接收的数据包。




**注意** 如果微型端口驱动程序未将 NDIS\_接收\_筛选器\_数据包\_合并\_筛选器\_启用标志，则驱动程序必须将**SupportedIUdpHeaderFields**成员设置为零。




11. 微型端口驱动程序必须报告可以为单个数据包合并筛选器指定的数据包标头字段上的最大测试数。 驱动程序在**MaxFieldTestsPerPacketCoalescingFilter**成员中指定此值。

    **注意** 支持数据包合并的网络适配器必须支持5个或更多可为单个数据包合并筛选器指定的数据包标头字段。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。



12. 微型端口驱动程序必须报告网络适配器所支持的数据包合并筛选器的最大数量。 驱动程序在**MaxPacketCoalescingFilters**成员中指定此值。

    **注意** 支持数据包合并的网络适配器必须支持10个或更多数据包合并筛选器。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。



当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序会按照以下步骤报告基础网络适配器的数据包合并和筛选功能：

-   微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    如果注册表中的 **\*PacketCoalescing**关键字设置的值为1，则微型端口驱动程序会将**HardwareReceiveFilterCapabilities**成员设置为指向先前初始化的[**NDIS\_接收的指针\_筛选\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

    如果注册表中的 **\*PacketCoalescing**关键字设置的值为零，则微型端口驱动程序不会播发对数据包合并的支持。 它必须将**HardwareReceiveFilterCapabilities**成员设置为 NULL。

-   驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

微型端口驱动程序用来报告基础网络适配器的数据包合并和筛选功能的方法基于用于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。
