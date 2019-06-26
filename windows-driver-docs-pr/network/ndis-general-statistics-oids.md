---
title: NDIS 常规统计信息 OID
description: 本部分介绍所有 NDIS 驱动程序的常规统计的信息 Oid
keywords:
- NDIS 常规统计信息 OID
- WDK NDIS 常规统计信息 Oid
- WDK 常规统计信息 Oid
ms.assetid: 364BEF6E-489C-427A-9ACC-D18F29F22B0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db4f4d8b24819adb10db7e8537f41db9e6e9a94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385518"
---
# <a name="ndis-general-statistics-oids"></a>NDIS 常规统计信息 OID

驱动程序应响应具有完整信息的 OID，以便该驱动程序的操作系统和应用程序使用来监视网络状态所需的信息可以提供响应的安全问题，统计信息的查询并诊断问题。 如果统计信息计数器在硬件中，该驱动程序应读取的相应统计信息值从硬件每次查询统计信息 OID。

## <a name="miniport-driver-support-for-64-bit-counters"></a>对 64 位计数器的微型端口驱动程序支持

所有 1 Gbps 和更快的微型端口驱动程序必须都支持 64 位计数器 Oid 的以下统计信息。 此外，Microsoft 建议，所有 100Mbps 和更快的微型端口驱动程序都支持 64 位计数器 Oid 的以下统计信息：

- [OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)
- [OID_GEN_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv)
- [OID_GEN_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit)
- [OID_GEN_RCV_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards)
- [OID_GEN_XMIT_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards)
- [OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)
- [OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)
- [OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)
- [OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)
- [OID_GEN_RCV_NO_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer)
- [OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)
- [OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)
- [OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)
- [OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)
- [OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)
- [OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)
- [OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)
- [OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)
- [OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)
- [OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)
- [OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)
- [OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)
- [OID_GEN_RCV_CRC_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error)
- [OID_GEN_TRANSMIT_QUEUE_LENGTH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length)
- [OID_GEN_INIT_TIME_MS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-init-time-ms)
- [OID_GEN_RESET_COUNTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-reset-counts)
- [OID_GEN_MEDIA_SENSE_COUNTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-sense-counts)

微型端口驱动程序还可以支持 64 位计数器的 Oid，如 Oid 指示传输或接收错误的其他统计信息。

系统支持的 64 位计数器是在 Windows XP 和更高版本操作系统中可用。

>[!NOTE]
> 如果 NDIS MUX 驱动程序将公开多个微型端口实例，查询以下常规统计信息 Oid 应返回数据特定于该微型端口实例。 例如，如果 MUX 驱动程序实现虚拟局域网 (VLAN) 筛选，并公开一个微型端口，每个 VLAN，从以下 Oid 返回统计信息值应为每个 VLAN。
> - [OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)
> - [OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)
> - [OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)


