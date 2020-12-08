---
title: NDIS 常规统计信息 OID
description: 本部分介绍所有 NDIS 驱动程序的常规统计信息 Oid
keywords:
- NDIS 常规统计信息 OID
- WDK NDIS 常规统计信息 Oid
- WDK 常规统计信息 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fe896da6e5cac24eb3810e7db5b3342b3404152
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803507"
---
# <a name="ndis-general-statistics-oids"></a>NDIS 常规统计信息 OID

驱动程序应该对统计信息 OID 查询进行响应，以提供完整的信息，以便驱动程序可以为操作系统和应用程序提供监视网络状态、响应安全问题和诊断问题所需的信息。 如果统计信息计数器在硬件中，则每次查询统计信息 OID 时，驱动程序都应从硬件读取相应的统计信息值。

## <a name="miniport-driver-support-for-64-bit-counters"></a>适用于64位计数器的微型端口驱动程序支持

对于以下统计信息 Oid，所有一个 Gbps 和更快的微型端口驱动程序都必须支持64位计数器。 此外，Microsoft 建议所有100Mbps 和更快速的微型端口驱动程序都支持以下统计信息 Oid 的64位计数器：

- [OID_GEN_STATISTICS](./oid-gen-statistics.md)
- [OID_GEN_BYTES_RCV](./oid-gen-bytes-rcv.md)
- [OID_GEN_BYTES_XMIT](./oid-gen-bytes-xmit.md)
- [OID_GEN_RCV_DISCARDS](./oid-gen-rcv-discards.md)
- [OID_GEN_XMIT_DISCARDS](./oid-gen-xmit-discards.md)
- [OID_GEN_XMIT_OK](./oid-gen-xmit-ok.md)
- [OID_GEN_RCV_OK](./oid-gen-rcv-ok.md)
- [OID_GEN_XMIT_ERROR](./oid-gen-xmit-error.md)
- [OID_GEN_RCV_ERROR](./oid-gen-rcv-error.md)
- [OID_GEN_RCV_NO_BUFFER](./oid-gen-rcv-no-buffer.md)
- [OID_GEN_DIRECTED_BYTES_XMIT](./oid-gen-directed-bytes-xmit.md)
- [OID_GEN_DIRECTED_FRAMES_XMIT](./oid-gen-directed-frames-xmit.md)
- [OID_GEN_MULTICAST_BYTES_XMIT](./oid-gen-multicast-bytes-xmit.md)
- [OID_GEN_MULTICAST_FRAMES_XMIT](./oid-gen-multicast-frames-xmit.md)
- [OID_GEN_BROADCAST_BYTES_XMIT](./oid-gen-broadcast-bytes-xmit.md)
- [OID_GEN_BROADCAST_FRAMES_XMIT](./oid-gen-broadcast-frames-xmit.md)
- [OID_GEN_DIRECTED_BYTES_RCV](./oid-gen-directed-bytes-rcv.md)
- [OID_GEN_DIRECTED_FRAMES_RCV](./oid-gen-directed-frames-rcv.md)
- [OID_GEN_MULTICAST_BYTES_RCV](./oid-gen-multicast-bytes-rcv.md)
- [OID_GEN_MULTICAST_FRAMES_RCV](./oid-gen-multicast-frames-rcv.md)
- [OID_GEN_BROADCAST_BYTES_RCV](./oid-gen-broadcast-bytes-rcv.md)
- [OID_GEN_BROADCAST_FRAMES_RCV](./oid-gen-broadcast-frames-rcv.md)
- [OID_GEN_RCV_CRC_ERROR](./oid-gen-rcv-crc-error.md)
- [OID_GEN_TRANSMIT_QUEUE_LENGTH](./oid-gen-transmit-queue-length.md)
- [OID_GEN_INIT_TIME_MS](./oid-gen-init-time-ms.md)
- [OID_GEN_RESET_COUNTS](./oid-gen-reset-counts.md)
- [OID_GEN_MEDIA_SENSE_COUNTS](./oid-gen-media-sense-counts.md)

小型端口驱动程序还可以支持用于其他统计信息 Oid 的64位计数器，例如指示传输或接收错误的 Oid。

Windows XP 和更高版本的操作系统中提供了64位计数器的系统支持。

>[!NOTE]
> 如果 NDIS MUX 驱动程序公开多个微型端口实例，则查询以下常规统计信息 Oid 应返回特定于该微型端口实例的数据。 例如，如果 MUX 驱动程序实现虚拟局域网 (VLAN) 筛选并公开每个 VLAN 的一个微型端口，则应根据 VLAN 从以下 Oid 返回统计信息值。
> - [OID_GEN_STATISTICS](./oid-gen-statistics.md)
> - [OID_GEN_RCV_OK](./oid-gen-rcv-ok.md)
> - [OID_GEN_XMIT_OK](./oid-gen-xmit-ok.md)
