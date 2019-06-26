---
title: 面向连接的微型端口驱动程序的常规统计信息 OID
description: 本主题介绍面向连接的对象的常规统计的信息 Oid。
ms.assetid: 1967ebb9-0cc9-46ca-b9db-fc505f41c38e
keywords:
- 常规统计信息 Oid 面向连接的微型端口驱动程序
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9396f31f7c0ee7dacdc985f71147d1b1c4cd5da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382766"
---
# <a name="general-statistics-oids-for-connection-oriented-miniport-drivers"></a>面向连接的微型端口驱动程序的常规统计信息 OID

下表总结了用于获取或设置面向连接的微型端口驱动程序的常规统计信息特征和/或其 Nic 的 Oid。

> [!TIP] 
> 面向连接的微型端口驱动程序将处理此类请求在其[MiniportCoOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)回调函数。

在此表中，M 指示 OID 是必需的而 O 则指示它是可选的。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 4 或 8 | O |   | [OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md) |
| 4 或 8 | O |   | [OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md) |
| 4 或 8 | O |   | [OID_GEN_CO_BYTES_XMIT_OUTSTANDING](oid-gen-co-bytes-xmit-outstanding.md) |
| 4 或 8 | O |   | [OID_GEN_CO_NETCARD_LOAD](oid-gen-co-netcard-load.md) |
| 4 或 8 | O |   | [OID_GEN_CO_RCV_CRC_ERROR](oid-gen-co-rcv-crc-error.md) |
| 4 或 8 | M |   | [OID_GEN_CO_RCV_PDUS_ERROR](oid-gen-co-rcv-pdus-error.md) |
| 4 或 8 | M |   | [OID_GEN_CO_RCV_PDUS_NO_BUFFER](oid-gen-co-rcv-pdus-no-buffer.md) |
| 4 或 8 | M |   | [OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md) |
| 4 或 8 | O |   | [OID_GEN_CO_TRANSMIT_QUEUE_LENGTH](oid-gen-co-transmit-queue-length.md) |
| 4 或 8 | M |   | [OID_GEN_CO_XMIT_PDUS_ERROR](oid-gen-co-xmit-pdus-error.md) |
| 4 或 8 | M |   | [OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md) |

## <a name="miniport-driver-support-for-64-bit-counters"></a>对 64 位计数器的微型端口驱动程序支持

所有 1 Gbps 和更快地面向连接的微型端口驱动程序必须都支持 64 位计数器 Oid 的以下统计信息。 此外，Microsoft 建议，所有 100Mbps 和更快的面向连接的 miiniport 驱动程序都支持 64 位计数器 Oid 的以下统计信息：

[OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md)

[OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md)

[OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md)

[OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md)

这种微型端口驱动程序还可以支持 64 位计数器的 Oid，如 Oid 指示传输或接收错误的其他统计信息。

对 64 位计数器的系统支持现已推出 Windows XP 及更高版本。

