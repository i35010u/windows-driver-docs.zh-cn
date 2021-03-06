---
title: RSS 哈希类型
description: RSS 哈希类型
keywords:
- 接收方缩放 WDK 网络，哈希
- RSS WDK 网络，哈希
- 哈希 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a70155665e3cb942770d5f16dc46bc64300bf1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248325"
---
# <a name="rss-hashing-types"></a>RSS 哈希类型

## <a name="overview"></a>概述

RSS 哈希类型指定接收的网络数据中 NIC 必须用于计算 RSS 哈希值的部分。

过量驱动程序设置哈希类型、函数和间接寻址表。 过量驱动程序集的哈希类型可以是微型端口驱动程序可以支持的类型的子集。 有关详细信息，请参阅 [RSS 配置](rss-configuration.md)。

哈希类型为或以下标志的有效组合：

- NDIS_HASH_IPV4
- NDIS_HASH_TCP_IPV4
- NDIS_HASH_UDP_IPV4
- NDIS_HASH_IPV6
- NDIS_HASH_TCP_IPV6
- NDIS_HASH_UDP_IPV6
- NDIS_HASH_IPV6_EX
- NDIS_HASH_TCP_IPV6_EX
- NDIS_HASH_UDP_IPV6_EX

这些是有效的标志组合集：

- IPv4 (NDIS_HASH_IPV4、NDIS_HASH_TCP_IPV4 和 NDIS_HASH_UDP_IPV4 的组合) 
- IPv6 (NDIS_HASH_IPV6、NDIS_HASH_TCP_IPV6 和 NDIS_HASH_UDP_IPV6 的组合) 
- 具有扩展标头的 IPv6 (NDIS_HASH_IPV6_EX、NDIS_HASH_TCP_IPV6_EX 和 NDIS_HASH_UDP_IPV6_EX 的组合) 

NIC 必须支持 IPv4 集中的其中一种组合。 其他集和组合是可选的。 一个 NIC 一次可以支持多个集。 在这种情况下，收到的数据类型决定了 NIC 使用的哈希类型。

通常，如果 NIC 无法正确解释收到的数据，则它不得计算哈希值。 例如，如果 NIC 只支持 IPv4 并且接收到无法正确解释的 IPv6 数据包，则它不得计算哈希值。 如果 NIC 接收到不支持的传输类型的数据包，则它不能计算哈希值。 例如，如果 NIC 收到的 UDP 数据包应为 TCP 数据包的哈希值，则它不能计算哈希值。 在这种情况下，数据包的处理方式与非 RSS 情况一样。 有关非 RSS 接收处理的详细信息，请参阅 [非 Rss 接收处理](non-rss-receive-processing.md)。

## <a name="ipv4-hash-type-combinations"></a>IPv4 哈希类型组合

IPv4 集中的有效哈希类型组合如下：

- [NDIS_HASH_IPV4](#ndis_hash_ipv4)
- [NDIS_HASH_TCP_IPV4](#ndis_hash_tcp_ipv4)
- [NDIS_HASH_UDP_IPV4](#ndis_hash_udp_ipv4)
- [NDIS_HASH_TCP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_tcp_ipv4--ndis_hash_ipv4)
- [NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_udp_ipv4--ndis_hash_ipv4)
- [NDIS_HASH_TCP_IPV4 |NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_tcp_ipv4--ndis_hash_udp_ipv4--ndis_hash_ipv4)

### <a name="ndis_hash_ipv4"></a><a name="ndis_hash_ipv4"></a> NDIS_HASH_IPV4  

如果设置了此标志，则 NIC 应计算以下 IPv4 标头字段的哈希值：

- 源-IPv4 地址
- 目标-IPv4 地址

>[!NOTE]
> 如果 NIC 收到包含 IP 和 TCP 标头的数据包，则不应始终使用 NDIS_HASH_TCP_IPV4。 对于分段 IP 数据包，必须使用 NDIS_HASH_IPV4。 这包括包含 IP 和 TCP 标头的第一个片段。

### <a name="ndis_hash_tcp_ipv4"></a><a name="ndis_hash_tcp_ipv4"></a> NDIS_HASH_TCP_IPV4

如果设置了此标志，则 NIC 应该分析收到的数据，以识别包含 TCP 段的 IPv4 数据包。

NIC 必须识别并跳过存在的任何 IP 选项。 如果 NIC 无法跳过任何 IP 选项，则不应计算哈希值。

NIC 应计算以下字段的哈希值：

- 源-IPv4 地址
- 目标-IPv4 地址
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndis_hash_udp_ipv4"></a><a name= "ndis_hash_udp_ipv4"></a> NDIS_HASH_UDP_IPV4

如果设置了此标志，则 NIC 应该分析收到的数据，以识别包含 UDP 数据报的 IPv4 数据包。

NIC 必须识别并跳过存在的任何 IP 选项。 如果 NIC 无法跳过任何 IP 选项，则不应计算哈希值。

NIC 应计算以下字段的哈希值：

- 源-IPv4 地址
- 目标-IPv4 地址
- 源 UDP 端口
- 目标 UDP 端口

### <a name="ndis_hash_tcp_ipv4--ndis_hash_ipv4"></a><a name="ndis_hash_tcp_ipv4--ndis_hash_ipv4"></a> NDIS_HASH_TCP_IPV4 |NDIS_HASH_IPV4

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_TCP_IPV4 用例指定的那样执行哈希计算。 但是，如果数据包不包含 TCP 标头，NIC 应计算为 NDIS_HASH_IPV4 用例指定的哈希值。

### <a name="ndis_hash_udp_ipv4--ndis_hash_ipv4"></a><a name="ndis_hash_udp_ipv4--ndis_hash_ipv4"></a> NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_UDP_IPV4 用例指定的那样执行哈希计算。 但是，如果数据包不包含 UDP 标头，NIC 应计算为 NDIS_HASH_IPV4 用例指定的哈希值。

### <a name="ndis_hash_tcp_ipv4--ndis_hash_udp_ipv4--ndis_hash_ipv4"></a><a name="ndis_hash_tcp_ipv4--ndis_hash_udp_ipv4--ndis_hash_ipv4"></a> NDIS_HASH_TCP_IPV4 |NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4

如果设置了此标志组合，则 NIC 应按照数据包中的传输指定的方式执行哈希计算。 但是，如果数据包不包含 TCP 或 UDP 标头，则 NIC 应计算为 NDIS_HASH_IPV4 用例指定的哈希值。

## <a name="ipv6-hash-type-combinations"></a>IPv6 哈希类型组合

IPv6 集中的有效哈希类型组合如下：

- [NDIS_HASH_IPV6](#ndis-hash-ipv6)
- [NDIS_HASH_TCP_IPV6](#ndis_hash_tcp_ipv6)
- [NDIS_HASH_UDP_IPV6](#ndis_hash_udp_ipv6)
- [NDIS_HASH_TCP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_tcp_ipv6--ndis_hash_ipv6)
- [NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_udp_ipv6--ndis_hash_ipv6)
- [NDIS_HASH_TCP_IPV6 |NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_tcp_ipv6--ndis_hash_udp_ipv6--ndis_hash_ipv6)

### <a name="ndis_hash_ipv6"></a><a name="ndis-hash-ipv6"></a> NDIS \_ 哈希 \_ IPV6

如果设置了此标志，则 NIC 应计算以下字段的哈希值：

- 源 IPv6 地址
- 目标-IPv6-地址

### <a name="ndis_hash_tcp_ipv6"></a><a name="ndis_hash_tcp_ipv6"></a> NDIS_HASH_TCP_IPV6

如果设置了此标志，则 NIC 应该分析收到的数据，以识别包含 TCP 段的 IPv6 数据包。 NIC 必须标识并跳过数据包中存在的任何 IPv6 扩展标头。 如果 NIC 无法跳过任何 IPv6 扩展标头，则不应计算哈希值。

NIC 应计算以下字段的哈希值：

- Source-IPv6 地址
- Destination-IPv6 地址
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndis_hash_udp_ipv6"></a><a name="ndis_hash_udp_ipv6"></a> NDIS_HASH_UDP_IPV6

如果设置了此标志，则 NIC 应该分析收到的数据，以识别包含 UDP 数据报的 IPv6 数据包。 NIC 必须标识并跳过数据包中存在的任何 IPv6 扩展标头。 如果 NIC 无法跳过任何 IPv6 扩展标头，则不应计算哈希值。

NIC 应计算以下字段的哈希值：

- 源 IPv6 地址
- 目标-IPv6-地址
- 源 UDP 端口
- 目标 UDP 端口

### <a name="ndis_hash_tcp_ipv6--ndis_hash_ipv6"></a><a name="ndis_hash_tcp_ipv6--ndis_hash_ipv6"></a>NDIS_HASH_TCP_IPV6 |NDIS_HASH_IPV6

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_TCP_IPV6 用例指定的那样执行哈希计算。 但是，如果数据包不包含 TCP 标头，NIC 应计算为 NDIS_HASH_IPV6 用例指定的哈希值。

例如，如果数据包有碎片，则它可能不包含 TCP 标头。  在这种情况下，NIC 只应计算 IP 标头的哈希值。

### <a name="ndis_hash_udp_ipv6--ndis_hash_ipv6"></a><a name="ndis_hash_udp_ipv6--ndis_hash_ipv6"></a> NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_UDP_IPV6 用例指定的那样执行哈希计算。 但是，如果数据包不包含 UDP 标头，NIC 应计算为 NDIS_HASH_IPV6 用例指定的哈希值。

例如，如果数据包有碎片，则它可能不包含 UDP 标头。  在这种情况下，NIC 只应计算 IP 标头的哈希值。

### <a name="ndis_hash_tcp_ipv6--ndis_hash_udp_ipv6--ndis_hash_ipv6"></a><a name="ndis_hash_tcp_ipv6--ndis_hash_udp_ipv6--ndis_hash_ipv6"></a> NDIS_HASH_TCP_IPV6 |NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6

如果设置了此标志组合，则 NIC 应按照数据包中的传输指定的方式执行哈希计算。 但是，如果数据包不包含 TCP 或 UDP 标头，则 NIC 应计算 NDIS_HASH_IPV6 用例中指定的哈希值。

例如，如果数据包有碎片，则它可能不包含 TCP 或 UDP 标头。  在这种情况下，NIC 只应计算 IP 标头的哈希值。

## <a name="ipv6-with-extension-headers-hash-type-combinations"></a>具有扩展标头的哈希类型组合的 IPv6

已设置的 IPv6 中的有效组合包括：

- [NDIS_HASH_IPV6_EX](#ndis_hash_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX](#ndis_hash_tcp_ipv6_ex)
- [NDIS_HASH_UDP_IPV6_EX](#ndis_hash_udp_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_tcp_ipv6_ex--ndis_hash_ipv6_ex)
- [NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_tcp_ipv6_ex--ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex)

### <a name="ndis_hash_ipv6_ex"></a><a name="ndis_hash_ipv6_ex"></a> NDIS_HASH_IPV6_EX  

如果设置了此标志，则 NIC 应计算以下字段的哈希值：

- 主地址从 "IPv6 目标选项" 标头中的 "家庭地址" 选项。 如果扩展插件标头不存在，请使用源 IPv6 地址。
- 包含在路由标头类型2中的 IPv6 地址（来自关联的扩展标头）。 如果扩展插件标头不存在，请使用目标 IPv6 地址。

### <a name="ndis_hash_tcp_ipv6_ex"></a><a name="ndis_hash_tcp_ipv6_ex"></a> NDIS_HASH_TCP_IPV6_EX

如果设置了此标志，则 NIC 应计算以下字段的哈希值：

- 主地址从 "IPv6 目标选项" 标头中的 "家庭地址" 选项。 如果扩展插件标头不存在，请使用源 IPv6 地址。
- 包含在路由标头类型2中的 IPv6 地址（来自关联的扩展标头）。 如果扩展插件标头不存在，请使用目标 IPv6 地址。
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndis_hash_udp_ipv6_ex"></a><a name="ndis_hash_udp_ipv6_ex"></a> NDIS_HASH_UDP_IPV6_EX

如果设置了此标志，则 NIC 应计算以下字段的哈希值：

- 主地址从 "IPv6 目标选项" 标头中的 "家庭地址" 选项。 如果扩展插件标头不存在，请使用源 IPv6 地址。
- 包含在路由标头类型2中的 IPv6 地址（来自关联的扩展标头）。 如果扩展插件标头不存在，请使用目标 IPv6 地址。
- 源 UDP 端口
- 目标 UDP 端口

### <a name="ndis_hash_tcp_ipv6_ex--ndis_hash_ipv6_ex"></a><a name="ndis_hash_tcp_ipv6_ex--ndis_hash_ipv6_ex"></a> NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_IPV6_EX

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_TCP_IPV6_EX 用例指定的那样执行哈希计算。 但是，如果数据包不包含 TCP 标头，NIC 应计算为 NDIS_HASH_IPV6_EX 用例指定的哈希值。

### <a name="ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a><a name="ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a> NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX

如果设置了此标志组合，NIC 应该按照为 NDIS_HASH_UDP_IPV6_EX 用例指定的那样执行哈希计算。 但是，如果数据包不包含 UDP 标头，NIC 应计算为 NDIS_HASH_IPV6_EX 用例指定的哈希值。

### <a name="ndis_hash_tcp_ipv6_ex--ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a><a name="ndis_hash_tcp_ipv6_ex--ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a> NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX

如果设置了此标志组合，NIC 应按照数据包传输的指定执行哈希计算。 但是，如果数据包不包含 TCP 或 UDP 标头，则 NIC 应计算为 NDIS_HASH_IPV6_EX 用例指定的哈希值。

> [!NOTE]
> 如果微型端口驱动程序报告 NIC NDIS_RSS_CAPS_HASH_TYPE_TCP_IPV6_EX 和/或 NDIS_RSS_CAPS_HASH_TYPE_UDP_IPV6_EX 功能，NIC 必须根据协议驱动程序设置的 IPv6 扩展哈希类型，计算 (IPv6 扩展标) 头中的字段的哈希值。 NIC 可以在为其计算哈希值的 IPv6 数据包的 NET_BUFFER_LIST 结构中存储扩展哈希类型或常规哈希类型。

微型端口驱动程序在指示收到的数据之前，在 [**NET_BUFFER_LIST**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构中设置哈希类型。 有关详细信息，请参阅 [指示 RSS 接收数据](indicating-rss-receive-data.md)。
