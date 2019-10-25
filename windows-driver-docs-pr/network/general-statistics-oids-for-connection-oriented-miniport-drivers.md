---
title: 面向连接的微型端口驱动程序的常规统计信息 OID
description: 本主题介绍面向连接的对象的常规统计信息 Oid。
ms.assetid: 1967ebb9-0cc9-46ca-b9db-fc505f41c38e
keywords:
- 常规统计信息 Oid 面向连接的小型端口驱动程序
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: aed8bc72c73eb155179e2dc3ab187aac1356430a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842187"
---
# <a name="general-statistics-oids-for-connection-oriented-miniport-drivers"></a>面向连接的微型端口驱动程序的常规统计信息 OID

下表总结了用于获取或设置面向连接的微型端口驱动程序和/或其 Nic 的常规统计特征的 Oid。

> [!TIP] 
> 面向连接的微型端口驱动程序在其[MiniportCoOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)回调函数中处理此类请求。

在此表中，M 指示 OID 是必需的，而 O 指示它是可选的。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 4或8 | O |   | [OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md) |
| 4或8 | O |   | [OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md) |
| 4或8 | O |   | [OID_GEN_CO_BYTES_XMIT_OUTSTANDING](oid-gen-co-bytes-xmit-outstanding.md) |
| 4或8 | O |   | [OID_GEN_CO_NETCARD_LOAD](oid-gen-co-netcard-load.md) |
| 4或8 | O |   | [OID_GEN_CO_RCV_CRC_ERROR](oid-gen-co-rcv-crc-error.md) |
| 4或8 | M |   | [OID_GEN_CO_RCV_PDUS_ERROR](oid-gen-co-rcv-pdus-error.md) |
| 4或8 | M |   | [OID_GEN_CO_RCV_PDUS_NO_BUFFER](oid-gen-co-rcv-pdus-no-buffer.md) |
| 4或8 | M |   | [OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md) |
| 4或8 | O |   | [OID_GEN_CO_TRANSMIT_QUEUE_LENGTH](oid-gen-co-transmit-queue-length.md) |
| 4或8 | M |   | [OID_GEN_CO_XMIT_PDUS_ERROR](oid-gen-co-xmit-pdus-error.md) |
| 4或8 | M |   | [OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md) |

## <a name="miniport-driver-support-for-64-bit-counters"></a>适用于64位计数器的微型端口驱动程序支持

对于以下统计信息 Oid，所有单 Gbps 和更快连接的微型端口驱动程序都必须支持64位计数器。 此外，Microsoft 建议所有100Mbps 和更快连接的 miiniport 驱动程序支持64位计数器，以进行以下统计信息 Oid：

[OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md)

[OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md)

[OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md)

[OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md)

此类微型端口驱动程序还可以支持64位计数器，用于其他统计信息 Oid，如指示传输或接收错误的 Oid。

Windows XP 和更高版本中提供了对64位计数器的系统支持。

