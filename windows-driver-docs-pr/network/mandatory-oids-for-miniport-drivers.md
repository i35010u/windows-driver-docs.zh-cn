---
title: 微型端口驱动程序的必需 OID
description: 本主题介绍必需 Oid 的微型端口驱动程序
ms.assetid: e4a620b4-de8f-4c1a-be94-b0ec97fa9791
keywords:
- 必需 Oid 微型端口驱动程序，请强制 NDIS Oid，必需的 Oid WDK 必需 Oid 网络
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a236c5de40c56374108cbbd45d89c22c089558c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343495"
---
# <a name="mandatory-oids-for-miniport-drivers"></a>微型端口驱动程序的必需 OID

下表列出了是强制性的所有微型端口驱动程序的 Oid。 将所需微型端口驱动程序以支持其他 Oid，具体取决于其 NDIS 版本和服务，它支持，例如：

- 面向连接的对象 
- CoNDIS  
- 以太网统计信息 OID 
- 标头数据拆分 Oid 
- Hyper-V 可扩展交换机 OID 
- IPsec 卸载版本 2 Oid 
- MB Oid 
- 本机 802.11 无线 LAN Oid 
- NDIS TCP/IP 卸载 Oid 
- NDKPI Oid 
- 操作电源管理 Oid 
- 接收筛选器 Oid 的概述 
- 接收筛选器 Oid 
- 接收方缩放 Oid 
- 远程 NDIS OID 
- 电源管理的必需和可选 OID 
- SR-IOV OID 
- 统计电源管理 Oid 
- 任务卸载对象 
- VMQ Oid

在表中的"O/M"列： 

- "M"表示"必需"，"O"表示"可选"。
- "O/M 的查询"列中的"不适用"意味着 NDIS 处理 OID 查询请求，并不会发送到微型端口驱动程序，因此微型端口驱动程序仅需要支持 OID 设置请求。 
- 如果"O/M 的查询"列中没有任何条目，此 OID 是仅限集的 OID。
- 如果"O/M 设置"列中没有任何条目，此 OID 是仅限查询的 OID。

| OID | O/M 查询 | O/M 的组 | 备注 |
| --- | --- | --- | --- |
| [OID_GEN_CURRENT_LOOKAHEAD](oid-gen-current-lookahead.md) | 不可用 | M | NDIS 处理查询和未成功的集请求的微型端口驱动程序。 NDIS 将有效的集请求发送到微型端口驱动程序。 你可以获取相同的信息与[OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md)。 |
| [OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md) | 不可用 | M | 查询不是必需的。 集是必需的。 |
| [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) | M | M |   |
| [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) |   | M |   |
| [OID_GEN_MAXIMUM_TOTAL_SIZE](oid-gen-maximum-total-size.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_RCV_OK](oid-gen-rcv-ok.md) | M |   | NDIS 不处理此 OID 的微型端口驱动程序和[OID_GEN_STATISTICS](oid-gen-statistics.md)不包括此信息。 **注意**：统计信息 Oid 是必需的除非 NDIS 处理它们。 |
| [OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md) | M |   | NDIS 不处理此 OID 的微型端口驱动程序。 |
| [OID_GEN_RECEIVE_BUFFER_SPACE](oid-gen-receive-buffer-space.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_STATISTICS](oid-gen-statistics.md) | M |   |   |
| [OID_GEN_TRANSMIT_BLOCK_SIZE](oid-gen-transmit-block-size.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_TRANSMIT_BUFFER_SPACE](oid-gen-transmit-buffer-space.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_VENDOR_DESCRIPTION](oid-gen-vendor-description.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_VENDOR_DRIVER_VERSION](oid-gen-vendor-driver-version.md) | M |   | 没有其他方法来获取此信息。 |
| [OID_GEN_VENDOR_ID](oid-gen-vendor-id.md) | M |   | 没有其他方法来获取此信息。 独立硬件供应商的筛选器驱动程序或中间驱动程序可以查询此 OID。 |
| [OID_GEN_XMIT_OK](oid-gen-xmit-ok.md) | M |   | NDIS 不处理此 OID 并[OID_GEN_STATISTICS](oid-gen-statistics.md)不包括此信息。 **注意**：统计信息 Oid 是必需的除非 NDIS 处理它们。 |

