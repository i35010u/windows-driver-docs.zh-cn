---
title: RSS 哈希类型
description: RSS 哈希类型
ms.assetid: 21ea384c-5fe2-46c1-9e01-30513f505672
keywords:
- 接收方缩放 WDK 网络，哈希
- RSS WDK 网络、 哈希
- 哈希 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 268a3e52cd8185554b1b151fa871413d9b406a77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372184"
---
# <a name="rss-hashing-types"></a>RSS 哈希类型

## <a name="overview"></a>概述

RSS 哈希算法类型指定 NIC 必须用来计算 RSS 哈希值的接收的网络数据的部分。

过量驱动程序设置哈希类型、 函数和间接表。 基础驱动程序设置的哈希类型可以是类型的微型端口驱动程序支持的子集。 有关详细信息，请参阅[RSS 配置](rss-configuration.md)。

哈希类型是 OR 的有效组合的以下标志：

- NDIS_HASH_IPV4
- NDIS_HASH_TCP_IPV4
- NDIS_HASH_UDP_IPV4
- NDIS_HASH_IPV6
- NDIS_HASH_TCP_IPV6
- NDIS_HASH_UDP_IPV6
- NDIS_HASH_IPV6_EX
- NDIS_HASH_TCP_IPV6_EX
- NDIS_HASH_UDP_IPV6_EX

以下是有效的标志组合的集：

- IPv4 （NDIS_HASH_IPV4、 NDIS_HASH_TCP_IPV4 和 NDIS_HASH_UDP_IPV4 的组合）
- IPv6 （NDIS_HASH_IPV6、 NDIS_HASH_TCP_IPV6 和 NDIS_HASH_UDP_IPV6 的组合）
- IPv6 扩展标头 （NDIS_HASH_IPV6_EX、 NDIS_HASH_TCP_IPV6_EX 和 NDIS_HASH_UDP_IPV6_EX 的组合）

NIC 必须支持从 IPv4 设置的组合之一。 其他设置和组合是可选的。 NIC 可以一次支持多个集。 在这种情况下，接收的数据类型确定哪些哈希类型 NIC 使用。

一般情况下，如果 NIC 无法正确解释接收到的数据，它必须计算的哈希值。 例如，如果 NIC 仅支持 IPv4 和接收 IPv6 数据包，它无法正确解释时，它必须计算的哈希值。 如果 NIC 会收到不支持的传输类型的数据包，必须计算的哈希值。 例如，如果 NIC 接收 UDP 数据包，当它应被计算 TCP 数据包的哈希值时，它必须计算的哈希值。 在这种情况下，非 RSS 一样处理数据包。 有关详细信息，有关非 RSS 接收处理，请参阅[处理非 RSS 接收](non-rss-receive-processing.md)。

## <a name="ipv4-hash-type-combinations"></a>IPv4 哈希类型组合

在 IPv4 集中的有效的哈希类型组合包括：

- [NDIS_HASH_IPV4](#ndishashipv4)
- [NDIS_HASH_TCP_IPV4](#ndishashtcpipv4)
- [NDIS_HASH_UDP_IPV4](#ndishashudpipv4)
- [NDIS_HASH_TCP_IPV4 | NDIS_HASH_IPV4](#ndishashtcpipv4--ndishashipv4)
- [NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4](#ndishashudpipv4--ndishashipv4)
- [NDIS_HASH_TCP_IPV4 | NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4](#ndishashtcpipv4--ndishashudpipv4--ndishashipv4)

### <a name="ndishashipv4"></a>NDIS_HASH_IPV4  

如果设置此标志仅，NIC 应针对以下 IPv4 标头字段计算的哈希值：

- Source-IPv4-Address
- Destination-IPv4-Address

>[!NOTE]
> 如果 NIC 收到的数据包，IP 和 TCP 标头，NDIS_HASH_TCP_IPV4 不始终应。 对于碎片 IP 数据包时，必须使用 NDIS_HASH_IPV4。 这包括其中包含 IP 和 TCP 标头的第一个片段。

### <a name="ndishashtcpipv4"></a>NDIS_HASH_TCP_IPV4

如果设置此标志仅，NIC 应分析接收到的数据来标识包含 TCP 段的 IPv4 数据包。

NIC 必须识别并跳过有任何 IP 选项。 如果 NIC 不能跳过任何 IP 选项，它应计算的哈希值。

NIC 应针对以下字段计算的哈希值：

- Source-IPv4-Address
- Destination-IPv4-Address
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndishashudpipv4"></a>NDIS_HASH_UDP_IPV4

如果设置此标志仅，NIC 应分析接收到的数据来标识包含 UDP 数据报的 IPv4 数据包。

NIC 必须识别并跳过有任何 IP 选项。 如果 NIC 不能跳过任何 IP 选项，它应计算的哈希值。

NIC 应针对以下字段计算的哈希值：

- Source-IPv4-Address
- Destination-IPv4-Address
- UDP 源端口
- 目标 UDP 端口

### <a name="ndishashtcpipv4--ndishashipv4"></a>NDIS_HASH_TCP_IPV4 | NDIS_HASH_IPV4

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_TCP_IPV4 用例。 但是，如果数据包不包含 TCP 标头，NIC 应计算 NDIS_HASH_IPV4 情况下为指定的哈希值。

### <a name="ndishashudpipv4--ndishashipv4"></a>NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_UDP_IPV4 用例。 但是，如果数据包不包含 UDP 标头，NIC 应计算 NDIS_HASH_IPV4 情况下为指定的哈希值。

### <a name="ndishashtcpipv4--ndishashudpipv4--ndishashipv4"></a>NDIS_HASH_TCP_IPV4 | NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4

如果设置此标志组合，NIC 应执行哈希计算指定的传输数据包中。 但是，如果数据包不包含 TCP 或 UDP 标头，NIC 应计算 NDIS_HASH_IPV4 情况下为指定的哈希值。

## <a name="ipv6-hash-type-combinations"></a>IPv6 哈希类型组合

在 IPv6 集中的有效的哈希类型组合包括：

- [NDIS_HASH_IPV6](#ndishashipv6)
- [NDIS_HASH_TCP_IPV6](#ndishashtcpipv6)
- [NDIS_HASH_UDP_IPV6](#ndishashudpipv6)
- [NDIS_HASH_TCP_IPV6 | NDIS_HASH_IPV6](#ndishashtcpipv6--ndishashipv6)
- [NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6](#ndishashudpipv6--ndishashipv6)
- [NDIS_HASH_TCP_IPV6 | NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6](#ndishashtcpipv6--ndishashudpipv6--ndishashipv6)

### <a name="ndishashipv6"></a>NDIS_HASH_IPV6

如果设置此标志仅，NIC 应针对以下字段计算哈希：

- Source-IPv6-Address
- Destination-IPv6-Address

### <a name="ndishashtcpipv6"></a>NDIS_HASH_TCP_IPV6

如果设置此标志仅，NIC 应分析接收到的数据来标识包含 TCP 段的 IPv6 数据包。 NIC 必须识别并跳过在包中存在任何 IPv6 扩展标头。 如果 NIC 不能跳过任何 IPv6 扩展标头，它应计算的哈希值。

NIC 应针对以下字段计算的哈希值：

- Source-IPv6 -Address
- 目标 IPv6 的地址
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndishashudpipv6"></a>NDIS_HASH_UDP_IPV6

如果设置此标志仅，NIC 应分析接收的数据，以识别 IPv6 数据包包含 UDP 数据报。 NIC 必须识别并跳过在包中存在任何 IPv6 扩展标头。 如果 NIC 不能跳过任何 IPv6 扩展标头，它应计算的哈希值。

NIC 应针对以下字段计算的哈希值：

- Source-IPv6-Address
- Destination-IPv6-Address
- UDP 源端口
- 目标 UDP 端口

### <a name="ndishashtcpipv6--ndishashipv6"></a>NDIS_HASH_TCP_IPV6 | NDIS_HASH_IPV6

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_TCP_IPV6 用例。 但是，如果数据包不包含 TCP 标头，NIC 应计算 NDIS_HASH_IPV6 情况下为指定的哈希。

### <a name="ndishashudpipv6--ndishashipv6"></a>NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_UDP_IPV6 用例。 但是，如果数据包不包含 UDP 标头，NIC 应计算 NDIS_HASH_IPV6 情况下为指定的哈希。

### <a name="ndishashtcpipv6--ndishashudpipv6--ndishashipv6"></a>NDIS_HASH_TCP_IPV6 | NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6

如果设置此标志组合，NIC 应执行哈希计算指定的传输数据包中。 但是，如果数据包不包含 TCP 或 UDP 标头，NIC 应计算 NDIS_HASH_IPV6 用例中所指定的哈希值。

## <a name="ipv6-with-extension-headers-hash-type-combinations"></a>扩展标头的哈希类型组合使用 IPv6

使用扩展标头集 IPv6 中的有效组合包括：

- [NDIS_HASH_IPV6_EX](#ndishashipv6ex)
- [NDIS_HASH_TCP_IPV6_EX](#ndishashtcpipv6ex)
- [NDIS_HASH_UDP_IPV6_EX](#ndishashudpipv6ex)
- [NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashtcpipv6ex--ndishashipv6ex)
- [NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashudpipv6ex--ndishashipv6ex)
- [NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashtcpipv6ex--ndishashudpipv6ex--ndishashipv6ex)

### <a name="ndishashipv6ex"></a>NDIS_HASH_IPV6_EX  

如果设置此标志仅，NIC 应针对以下字段计算哈希：

- 从 IPv6 目标选项标头中的家庭地址选项的家庭地址。 如果扩展标头不存在，使用源 IPv6 地址。
- 路由的标头的类型 2 从关联的扩展标头中包含的 IPv6 地址。 如果扩展标头不存在，则使用目标 IPv6 地址。

### <a name="ndishashtcpipv6ex"></a>NDIS_HASH_TCP_IPV6_EX

如果设置此标志仅，NIC 应针对以下字段计算哈希：

- 从 IPv6 目标选项标头中的家庭地址选项的家庭地址。 如果扩展标头不存在，使用源 IPv6 地址。
- 路由的标头的类型 2 从关联的扩展标头中包含的 IPv6 地址。 如果扩展标头不存在，则使用目标 IPv6 地址。
- 源 TCP 端口
- 目标 TCP 端口

### <a name="ndishashudpipv6ex"></a>NDIS_HASH_UDP_IPV6_EX

如果设置此标志仅，NIC 应针对以下字段计算哈希：

- 从 IPv6 目标选项标头中的家庭地址选项的家庭地址。 如果扩展标头不存在，使用源 IPv6 地址。
- 路由的标头的类型 2 从关联的扩展标头中包含的 IPv6 地址。 如果扩展标头不存在，则使用目标 IPv6 地址。
- UDP 源端口
- 目标 UDP 端口

### <a name="ndishashtcpipv6ex--ndishashipv6ex"></a>NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_IPV6_EX

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_TCP_IPV6_EX 用例。 但是，如果数据包不包含 TCP 标头，NIC 应计算 NDIS_HASH_IPV6_EX 情况下为指定的哈希。

### <a name="ndishashudpipv6ex--ndishashipv6ex"></a>NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX

如果设置此标志组合，NIC 应执行指定的哈希计算 NDIS_HASH_UDP_IPV6_EX 用例。 但是，如果数据包不包含 UDP 标头，NIC 应计算 NDIS_HASH_IPV6_EX 情况下为指定的哈希。

### <a name="ndishashtcpipv6ex--ndishashudpipv6ex--ndishashipv6ex"></a>NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX

如果设置此标志组合，NIC 应执行的数据包传输由指定的哈希计算。 但是，如果数据包不包含 TCP 或 UDP 标头，NIC 应计算 NDIS_HASH_IPV6_EX 情况下为指定的哈希。

> [!NOTE]
> 如果微型端口驱动程序报告 NDIS_RSS_CAPS_HASH_TYPE_TCP_IPV6_EX 和/或 NDIS_RSS_CAPS_HASH_TYPE_UDP_IPV6_EX 功能的 nic，NIC 必须计算哈希值 （通过 IPv6 扩展标头中的字段） 根据 IPv6 扩展哈希类型协议驱动程序设置。 NIC 可以扩展哈希类型或常规哈希类型存储为其计算哈希值的 IPv6 数据包 NET_BUFFER_LIST 结构中。 

微型端口驱动程序设置中的哈希类型[ **NET_BUFFER_LIST** ](https://msdn.microsoft.com/library/windows/hardware/ff568388)之前，该值指示接收到的数据结构。 有关详细信息，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。

 

 





