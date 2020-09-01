---
title: UDP-ESP SA 和分析器项
description: UDP-ESP SA 和分析器项
ms.assetid: 1682b077-07ba-4b2e-9c01-fd7662f3f189
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载，分析器条目
- 分析器条目 WDK IPsec 卸载
- UDP 封装的 ESP 数据包 WDK IPsec 卸载，安全关联
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced2481501bebffb9511348fdca72fcedf82a13f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215783"
---
# <a name="udp-esp-sas-and-parser-entries"></a>UDP-ESP SA 和分析器项

\[IPsec 任务卸载功能已弃用，不应使用。\]




支持 UDP ESP 封装的微型端口驱动程序必须维护分析器条目的列表。 分析器条目包含 NIC 用于分析卸载的安全关联上的 UDP ESP 数据包 (SAs) 的信息。

分析器项包含以下信息：

-   UDP-ESP 封装类型。

    目前仅支持一个封装类型。 有关基本 UDP-ESP 封装类型的说明，请参阅 [UDP-Esp 封装类型](udp-esp-encapsulation-types.md)。

-   目标封装端口。

    NIC 应在其在卸载的 SAs 上处理的入站 UDP 封装的数据包的 UDP 标头中查找目标端口。 目前，仅端口4500支持 ESP 数据包的 UDP 封装。

TCP/IP 传输维护其自己的分析器条目列表，并将其卸载到微型端口驱动程序。 添加或删除 UDP ESP SA 时，传输和微型端口驱动程序会使用一个句柄来标识特定的分析器条目。

请注意，分析器条目允许扩展 UDP ESP 功能（如有必要）以适应不同的封装类型和每个封装类型的多个端口。

### <a name="adding-a-udp-esp-sa-and-parser-entry"></a>添加 UDP ESP SA 和分析器条目

TCP/IP 传输请求一个微型端口驱动程序，以便添加一个或多个 UDP ESP SAs，并通过发出 [OID \_ TCP \_ 任务 \_ IPSEC \_ add \_ UDPESP \_ SA](./oid-tcp-task-ipsec-add-udpesp-sa.md) 请求来添加此 sa 的分析器条目。 卸载**EncapTypeEntry** \_ IPSEC \_ ADD \_ UDPESP SA 结构的 EncapTypeEntry 成员 \_ 包含分析器条目信息。

在发出 OID \_ TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求之前，tcp/ip 传输会确定正在卸载的 SAs 的分析器条目是否位于指定 IP 接口的分析器条目列表中。

-   如果分析器项不在传输列表中，则传输将创建其自己的条目副本，并将卸载**EncapTypeEntryOffloadHandle** \_ IPSEC \_ ADD UDPESP SA 结构的 EncapTypeEntryOffloadHandle 成员设置 \_ \_ 为**NULL**。 然后，传输颁发 [OID \_ TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA](./oid-tcp-task-ipsec-add-udpesp-sa.md) 请求。 收到请求后，微型端口驱动程序将确定 **EncapTypeEntry** 指定的分析器条目是否位于 NIC 的分析器条目列表中。

    -   如果指定的分析器条目不在 NIC 的分析器条目列表中，微型端口驱动程序将使用 **EncapTypeEntry** 中指定的封装类型和目标端口创建分析器条目，并将该分析器条目添加到 NIC 的分析器条目列表。 然后，微型端口驱动程序会卸载 OID \_ TCP 任务 " \_ \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求" 中指定的 SAs。 成功完成 OID 请求后，微型端口驱动程序会在 **EncapTypeEntryOffloadHandle** 中返回一个用于标识新创建的分析器条目的句柄。 微型端口驱动程序还返回一个句柄，该句柄标识**OffloadHandle**卸载 \_ IPSEC \_ ADD \_ UDPESP \_ SA 结构的 OffloadHandle 成员中的已卸载的 SAs。
    -   如果指定的分析器条目已在 NIC 的分析器条目列表中，则微型端口驱动程序只返回现有分析器条目的 **EncapTypeEntryOffloadHandle** 中的句柄。 微型端口驱动程序还返回一个句柄，该句柄标识**OffloadHandle**卸载 \_ IPSEC \_ ADD \_ UDPESP \_ SA 结构的 OffloadHandle 成员中的已卸载的 SAs。

    如果微型端口驱动程序 \_ 已成功完成 OID TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求，则传输会将其新分析器条目的副本添加到其自己的给定 IP 接口的分析器条目列表。 此外，传输会递增分析器项的引用计数。 传输使用此引用计数来枚举与分析器条目关联的卸载 UDP ESP SAs 的数量。

    如果微型端口驱动程序无法进行 OID \_ TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求，则该传输会丢弃其分析器条目的副本。 如果微型端口驱动程序导致请求失败，则它必须确保它没有添加分析器条目并卸载 SAs。

-   如果分析器条目已在传输的分析器条目列表中，则微型端口驱动程序已经添加了分析器条目，以响应以前的 OID \_ TCP \_ 任务 " \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求"。 在这种情况下，传输会将分析器项的引用计数递增一，并将 **EncapTypeEntryOffloadHandle** 设置为微型端口驱动程序之前返回的值。 然后，传输颁发 OID \_ TCP \_ 任务 \_ IPSEC \_ ADD \_ UDPESP \_ SA 请求，这会请求微型端口驱动程序使用现有的分析器条目作为正在卸载的其他 SAs。 在这种情况下，微型端口驱动程序应该只返回标识已卸载的 SAs 的 **OffloadHandle** 。 如果 OID \_ TCP \_ 任务 " \_ IPSEC \_ ADD \_ UDPESP \_ SA" 请求失败，则传输将减少分析器条目的引用计数。

### <a name="deleting-a-udp-esp-sa-and-parser-entry"></a>删除 UDP ESP SA 和分析器条目

TCP/IP 传输请求一个微型端口驱动程序，以删除一个或多个 SAs，并可能通过发出 [OID \_ TCP \_ 任务 \_ IPSEC \_ delete \_ UDPESP \_ SA](./oid-tcp-task-ipsec-delete-udpesp-sa.md) 请求来删除这些 sas 的分析器条目。

发出此请求之前，TCP/IP 传输会将与要删除的 SAs 关联的分析器条目的引用计数递减。 然后，传输测试引用计数是否为零。

-   如果引用计数不为零，则分析器项与一个或多个当前卸载了 NIC 的其他 SAs 关联。 在这种情况下，传输将**EncapTypeEntryOffldHandle**卸载 \_ IPSEC \_ DELETE UDPESP SA 结构的 EncapTypeEntryOffldHandle 成员设置 \_ \_ 为**NULL**。 在收到 OID \_ tcp \_ 任务 \_ ipsec \_ delete \_ UDPESP \_ sa 请求后，微型端口驱动程序只会删除在 OID \_ tcp \_ 任务 \_ ipsec \_ delete \_ UDPESP \_ SA 请求中指定的 SAs。

-   如果引用计数为零，则分析器条目将不与已卸载到 NIC 的任何其他 SAs 关联。 在这种情况下，传输将 **EncapTypeEntryOffldHandle** 成员设置为微型端口驱动程序之前返回的分析器项句柄的值。 微型端口驱动程序删除指定的分析器条目和指定的 SAs。

如果微型端口驱动程序无法 \_ 执行 OID TCP \_ 任务 \_ IPSEC \_ DELETE \_ UDPESP \_ SA 请求，则它应将指定的 SAs （如果适用）标记为要删除的指定分析器条目，稍后再执行删除操作。 若要处理传入数据包，微型端口驱动程序不得使用标记为要删除的分析器条目或 SA。

请注意，在微型端口驱动程序添加该 SA 或分析器条目 (或两者) 之前，传输可能会请求使用微型端口驱动程序删除 SA 或分析器条目 (或两) 。 因此，微型端口驱动程序必须将删除操作与加法运算序列化。

 

