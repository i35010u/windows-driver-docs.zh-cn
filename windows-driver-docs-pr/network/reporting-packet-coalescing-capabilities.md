---
title: 报告数据包合并功能
description: 报告数据包合并功能
ms.assetid: 6118F648-87FE-4B9E-9535-1602F4FF79D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec920d2d8e1919d060abf50acf1b760541674cf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544894"
---
# <a name="reporting-packet-coalescing-capabilities"></a>报告数据包合并功能


微型端口驱动程序注册 NDIS 网络适配器初始化过程的以下功能：

-   网络适配器支持数据包合并功能。

-   网络适配器当前已启用数据包合并功能。

-   数据包合并接收的网络适配器当前已启用的筛选功能。

**请注意**数据包合并的微型端口驱动程序支持可启用或禁用通过 **\*PacketCoalescing** INF 关键字设置。 此设置显示在**高级**网络适配器的属性页。 有关数据包合并 INF 文件设置的详细信息，请参阅[数据包合并标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)。



微型端口驱动程序报告合并和筛选功能，通过基础的网络适配器的数据包[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。 如果 **\*PacketCoalescing**注册表中的关键字设置具有值 1、 数据包合并已启用并且微型端口驱动程序初始化**NDIS\_接收\_筛选器\_功能**结构如下所示：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

    如果该驱动程序支持数据包合并，则将设置**修订**的成员**标头**到 NDIS\_接收\_筛选器\_功能\_修订\_2，**大小**成员添加到 NDIS\_SIZEOF\_接收\_筛选器\_功能\_修订\_2。

2.  微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_支持\_ON\_默认\_中的队列标志**SupportedQueueProperties**成员。

    如果设置此标志，网络适配器必须支持硬件中接收多路广播数据包的筛选。 此筛选基于 NDIS 卸载到网络适配器发送的多播地址[OID\_802\_3\_多播\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569073)OID 设置请求。

    **请注意**协议驱动程序还可以通过发送更改多播的地址列表的内容[OID\_802\_3\_添加\_多播\_地址](https://msdn.microsoft.com/library/windows/hardware/ff569068)并[OID\_802\_3\_删除\_多播\_地址](https://msdn.microsoft.com/library/windows/hardware/ff569070)请求。 NDIS 将合并到这些请求[OID\_802\_3\_多播\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569073)OID 设置请求。




**请注意**是否需要拒绝任何传入的多路广播的数据包的目标媒体访问控制 (MAC) 地址不匹配任何这些 OID 集请求指定的多播地址的适配器。




3.  微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_中的已启用标志**EnabledFilterTypes**成员.

    **请注意**驱动程序设置此标志，如果它还必须设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_支持\_ON\_默认\_中的队列标志**SupportedQueueProperties**成员。 否则，NDIS 将失败的调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)通过返回 NDIS\_状态\_错误\_特征。



4.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，该驱动程序必须接收所有支持的筛选器测试条件。 该驱动程序通过设置以下标志播发此支持**SupportedFilterTests**成员：

    -   NDIS\_RECEIVE\_FILTER\_TEST\_HEADER\_FIELD\_EQUAL\_SUPPORTED

    -   NDIS\_RECEIVE\_FILTER\_TEST\_HEADER\_FIELD\_MASK\_EQUAL\_SUPPORTED

    -   NDIS\_RECEIVE\_FILTER\_TEST\_HEADER\_FIELD\_NOT\_EQUAL\_SUPPORTED

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedFilterTests**为零的成员。



5.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持在各种数据的筛选字段的媒体访问控制 (MAC)、 IP 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 标头。 该驱动程序通过设置以下标志播发此支持**SupportedHeaders**成员：

    -   NDIS\_接收\_筛选器\_MAC\_标头\_支持

    -   NDIS\_接收\_筛选器\_ARP\_标头\_支持

    -   NDIS\_RECEIVE\_FILTER\_IPV4\_HEADER\_SUPPORTED

    -   NDIS\_RECEIVE\_FILTER\_IPV6\_HEADER\_SUPPORTED

    -   NDIS\_RECEIVE\_FILTER\_UDP\_HEADER\_SUPPORTED

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedHeaders**为零的成员。



6.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持在媒体中的数据的筛选所接收数据包的访问控制 (MAC) 标头。 该驱动程序通过设置以下标志播发此支持**SupportedMacHeaderFields**成员：

    -   NDIS\_RECEIVE\_FILTER\_MAC\_HEADER\_DEST\_ADDR\_SUPPORTED

    -   NDIS\_接收\_筛选器\_MAC\_标头\_协议\_支持

    -   NDIS\_接收\_筛选器\_MAC\_标头\_数据包\_类型\_支持

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedMacHeaderFields**为零的成员。



7.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持中的数据筛选接收到的地址解析协议 (ARP) 数据包的标头。 该驱动程序通过设置以下标志播发此支持**SupportedARPHeaderFields**成员：

    -   NDIS\_接收\_筛选器\_ARP\_标头\_操作\_支持

    -   NDIS\_接收\_筛选器\_ARP\_标头\_SPA\_支持

    -   NDIS\_接收\_筛选器\_ARP\_标头\_TPA\_支持

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedARPHeaderFields**为零的成员。



8.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持打开中的数据筛选系统互连 (OSI) 层 3 (L3) 标头的接收 IP 版本 4 (IPv4) 数据包。 该驱动程序通过设置以下标志播发此支持**SupportedIPv4HeaderFields**成员：

    -   NDIS\_RECEIVE\_FILTER\_IPV4\_HEADER\_PROTOCOL\_SUPPORTED

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedIPv4HeaderFields**为零的成员。



9.  如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持的 L3 中的数据筛选标头的接收 IP 版本 6 (IPv6) 数据包。 该驱动程序通过设置以下标志播发此支持**SupportedIPv6HeaderFields**成员：

    -   NDIS\_RECEIVE\_FILTER\_IPV6\_HEADER\_PROTOCOL\_SUPPORTED

    **请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedIPv6HeaderFields**为零的成员。



10. 如果微型端口驱动程序设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标志，微型端口驱动程序必须支持 OSI 中的数据筛选层接收的用户数据报协议 (UDP) 数据包的 4 (L4) 标头。 该驱动程序通过设置以下标志播发此支持**SupportedIUdpHeaderFields**成员：

    -   NDIS\_RECEIVE\_FILTER\_UDP\_HEADER\_DEST\_PORT\_SUPPORTED

    **请注意**像它未通过 UDP 筛选器测试接收的 UDP 数据包中包含 IPv4 选项或 IPv6 扩展标头，如果网络适配器可以处理该数据包。 这样一来，适配器会自动删除所接收的数据包。




**请注意**如果微型端口驱动程序不会设置 NDIS\_接收\_筛选器\_数据包\_COALESCING\_筛选器\_已启用标记，该驱动程序必须设置**SupportedIUdpHeaderFields**为零的成员。




11. 微型端口驱动程序必须报告上数据包标头字段，可以指定单个数据包合并筛选器的测试的最大数目。 该驱动程序指定此值以**MaxFieldTestsPerPacketCoalescingFilter**成员。

    **请注意**支持数据包合并的网络适配器必须支持为单个数据包合并筛选器可以指定的五个或多个数据包标头字段。 如果适配器不支持合并的数据包，微型端口驱动程序必须将此值设置为零。



12. 微型端口驱动程序必须报告支持的网络适配器的数据包合并筛选器的最大数目。 该驱动程序指定此值以**MaxPacketCoalescingFilters**成员。

    **请注意**支持数据包合并的网络适配器必须支持 10 个或多个数据包合并筛选器。 如果适配器不支持合并的数据包，微型端口驱动程序必须将此值设置为零。



当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序报告合并和筛选功能的基础网络适配器的遵循这些数据包步骤：

-   微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

    如果 **\*PacketCoalescing**注册表中的关键字设置的值为一个微型端口驱动程序集**HardwareReceiveFilterCapabilities**成员是指向以前初始化[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

    如果 **\*PacketCoalescing**注册表中的关键字设置的值为零、 微型端口驱动程序不播发对数据包合并的支持。 必须设置**HardwareReceiveFilterCapabilities**为 NULL 的成员。

-   驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

微型端口驱动程序用于报告合并和筛选功能的基础网络适配器的数据包的方法基于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。
