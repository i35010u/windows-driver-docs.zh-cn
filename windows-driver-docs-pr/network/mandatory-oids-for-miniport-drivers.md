---
title: 微型端口驱动程序的必需 OID
description: 本主题介绍微型端口驱动程序的必需 Oid
keywords:
- 小型端口驱动程序的必需 Oid，必需的 NDIS Oid，必需的 Oid WDK，必需的 Oid 网络
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad1a12578291e05bec854cdb7348a3d28991116
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833361"
---
# <a name="mandatory-oids-for-miniport-drivers"></a>微型端口驱动程序的必需 OID

下表列出了所有微型端口驱动程序的必需 Oid。 需要你的微型端口驱动程序来支持其他 Oid，具体取决于其 NDIS 版本和它支持的服务，例如：

- Connection-Oriented 对象 
- CoNDIS  
- 以太网统计信息 OID 
- Header-Data 拆分 Oid 
- Hyper-V 可扩展交换机 OID 
- IPsec 卸载版本 2 Oid 
- MB Oid 
- 本机802.11 无线 LAN Oid 
- NDIS TCP/IP 卸载 Oid 
- NDKPI Oid 
- 操作电源管理 Oid 
- 接收筛选器 Oid 概述 
- 接收筛选 Oid 
- 接收方缩放 Oid 
- 远程 NDIS OID 
- 电源管理的必需和可选 OID 
- SR-IOV OID 
- 统计电源管理 Oid 
- 任务卸载对象 
- VMQ Oid

在表中的 "O/M" 列中： 

- "M" 表示 "必需" 和 "O" 表示 "可选"。
- 在 "O/M for Query" 列中，"N/A" 表示 NDIS 处理 OID 查询请求，但不将其发送到微型端口驱动程序，因此微型端口驱动程序只需支持 OID 设置请求。 
- 如果在 "O/M for Query" 列中没有任何条目，则此 OID 为仅限集的 OID。
- 如果在 "设置" 列的 "O/M" 列中没有任何条目，则此 OID 为仅查询 OID。

| OID | 查询的 O/M | 用于集的 O/M | 注释 |
| --- | --- | --- | --- |
| [OID_GEN_CURRENT_LOOKAHEAD](oid-gen-current-lookahead.md) | 空值 | M | NDIS 处理微型端口驱动程序的查询和设置失败的请求。 NDIS 将有效的 Set 请求发送到微型端口驱动程序。 您可以与 [OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md)获取相同的信息。 |
| [OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md) | 空值 | M | 查询不是必需的。 集是必需的。 |
| [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) | M | M |   |
| [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) |   | M |   |
| [OID_GEN_MAXIMUM_TOTAL_SIZE](oid-gen-maximum-total-size.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_RCV_OK](oid-gen-rcv-ok.md) | M |   | NDIS 不处理微型端口驱动程序的此 OID， [OID_GEN_STATISTICS](oid-gen-statistics.md) 不包括此信息。 **注意**：统计信息 oid 是必需的，除非 NDIS 处理它们。 |
| [OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md) | M |   | NDIS 不处理微型端口驱动程序的此 OID。 |
| [OID_GEN_RECEIVE_BUFFER_SPACE](oid-gen-receive-buffer-space.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_STATISTICS](oid-gen-statistics.md) | M |   |   |
| [OID_GEN_TRANSMIT_BLOCK_SIZE](oid-gen-transmit-block-size.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_TRANSMIT_BUFFER_SPACE](oid-gen-transmit-buffer-space.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_VENDOR_DESCRIPTION](oid-gen-vendor-description.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_VENDOR_DRIVER_VERSION](oid-gen-vendor-driver-version.md) | M |   | 没有其他方法可获取此信息。 |
| [OID_GEN_VENDOR_ID](oid-gen-vendor-id.md) | M |   | 没有其他方法可获取此信息。 独立硬件供应商的筛选器驱动程序或中间驱动程序可能会查询此 OID。 |
| [OID_GEN_XMIT_OK](oid-gen-xmit-ok.md) | M |   | NDIS 不处理此 OID， [OID_GEN_STATISTICS](oid-gen-statistics.md) 不包括此信息。 **注意**：统计信息 oid 是必需的，除非 NDIS 处理它们。 |

