---
title: 查询或设置信息
description: 查询或设置信息
keywords:
- 查询面向连接的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f4fab0f8ed5365f2f2298e40120c686ab8cb263
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820039"
---
# <a name="querying-or-setting-information"></a>查询或设置信息





CoNDIS protocol 驱动程序和 NDIS 可以将 OID 请求发送到底层驱动程序。  (MCMs) 的 CoNDIS 协议驱动程序和微型端口呼叫管理器还可以将 OID 请求发送到其他协议驱动程序。

面向连接的客户端或调用管理器调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 来查询或设置由绑定上的另一个协议驱动程序或基础微型端口驱动程序维护的信息。

在调用 **NdisCoOidRequest** 之前，客户端或调用管理器会为其请求分配一个缓冲区，并初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构。 此结构指定请求的类型 (查询或设置) ，标识查询或设置的 (OID) 的信息，以及指向用于传递 OID 数据的缓冲区。

如果面向连接的客户端或调用管理器传递了有效的 *NdisAfHandle* (请参阅 [地址系列](address-families.md)) ，NDIS 会调用绑定上每个协议驱动程序的 [**ProtocolCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_oid_request) 函数。

NDIS 定义对象标识符 (OID) 值标识适配器参数，其中包括操作参数，如设备特征、可配置设置和统计信息。 有关 Oid 的详细信息，请参阅 [NDIS oid](/windows-hardware/drivers/ddi/_netvista/)。

本节包括下列主题：

[CoNDIS 微型端口驱动程序 OID 请求](condis-miniport-driver-oid-requests.md)

[CoNDIS 协议驱动程序 OID 请求](condis-protocol-driver-oid-requests.md)

[CoNDIS MCM OID 请求](condis-mcm-oid-requests.md)

 

