---
title: NDIS 常规统计信息 Oid
description: 本部分介绍所有 NDIS 驱动程序的常规统计的信息 Oid
keywords:
- NDIS 常规统计信息 Oid
- WDK NDIS 常规统计信息 Oid
- WDK 常规统计信息 Oid
ms.assetid: 364BEF6E-489C-427A-9ACC-D18F29F22B0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a6b69fb0666debcc5a2b7700e3483970e7b3309
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540516"
---
# <a name="ndis-general-statistics-oids"></a>NDIS 常规统计信息 Oid

驱动程序应响应具有完整信息的 OID，以便该驱动程序的操作系统和应用程序使用来监视网络状态所需的信息可以提供响应的安全问题，统计信息的查询并诊断问题。 如果统计信息计数器在硬件中，该驱动程序应读取的相应统计信息值从硬件每次查询统计信息 OID。

## <a name="miniport-driver-support-for-64-bit-counters"></a>对 64 位计数器的微型端口驱动程序支持

所有 1 Gbps 和更快的微型端口驱动程序必须都支持 64 位计数器 Oid 的以下统计信息。 此外，Microsoft 建议，所有 100Mbps 和更快的微型端口驱动程序都支持 64 位计数器 Oid 的以下统计信息：

- [OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)
- [OID_GEN_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569443)
- [OID_GEN_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569445)
- [OID_GEN_RCV_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569628)
- [OID_GEN_XMIT_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569653)
- [OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)
- [OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)
- [OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)
- [OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)
- [OID_GEN_RCV_NO_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff569631)
- [OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)
- [OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)
- [OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)
- [OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)
- [OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)
- [OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)
- [OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)
- [OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)
- [OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)
- [OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)
- [OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)
- [OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)
- [OID_GEN_RCV_CRC_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569627)
- [OID_GEN_TRANSMIT_QUEUE_LENGTH](https://msdn.microsoft.com/library/windows/hardware/ff569646)
- [OID_GEN_INIT_TIME_MS](https://msdn.microsoft.com/library/windows/hardware/ff569588)
- [OID_GEN_RESET_COUNTS](https://msdn.microsoft.com/library/windows/hardware/ff569638)
- [OID_GEN_MEDIA_SENSE_COUNTS](https://msdn.microsoft.com/library/windows/hardware/ff569608)

微型端口驱动程序还可以支持 64 位计数器的 Oid，如 Oid 指示传输或接收错误的其他统计信息。

系统支持的 64 位计数器是在 Windows XP 和更高版本操作系统中可用。

>[!NOTE]
> 如果 NDIS MUX 驱动程序将公开多个微型端口实例，查询以下常规统计信息 Oid 应返回数据特定于该微型端口实例。 例如，如果 MUX 驱动程序实现虚拟局域网 (VLAN) 筛选，并公开一个微型端口，每个 VLAN，从以下 Oid 返回统计信息值应为每个 VLAN。
> - [OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)
> - [OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)
> - [OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)


