---
title: 查询 64 位统计信息 OID
description: 查询 64 位统计信息 OID
ms.assetid: dc43c33d-12a7-4468-9980-a9015f43e068
keywords:
- 统计信息 Oid WDK 网络
- 64位统计信息 Oid WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e4e8f9ff528d7fcd4ebdfa61e1c7bce3d635a07
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215146"
---
# <a name="querying-64-bit-statistics-oids"></a>查询 64 位统计信息 OID


每秒 1 Gb 到 (Gbps) 且速度更快的所有微型端口驱动程序必须支持特定统计信息 Oid 的64位计数器。 每秒100兆字节/秒 (Mbps) 和更快的微型端口驱动程序应支持此类 Oid 的64位计数器。 有关无连接微型端口驱动程序的统计信息 Oid 的详细信息，请参阅 [常规统计](./ndis-general-statistics-oids.md)信息。 有关面向连接的微型端口驱动程序的此类 Oid 的详细信息，请参阅 [面向连接的微型端口驱动程序的常规统计](./general-statistics-oids-for-connection-oriented-miniport-drivers.md)信息。

查询统计信息 OID 的请求者将 NDIS \_ OID \_ 请求 **InformationBufferLength** 设置为4个 (字节) 以指示32位统计请求，或设置为8个 (字节) 以指示64位统计请求。 在响应中，微型端口驱动程序会将 NDIS \_ OID \_ 请求 **BytesNeeded** 设置为微型端口驱动程序支持的统计信息值的大小，以使 64) 的32位或 8 (4。 微型端口驱动程序将 NDIS \_ OID \_ 请求 **BytesWritten** 设置为 **InformationBufferLength** 值较小的值，以及微型端口驱动程序所支持的统计信息的大小。

以下部分介绍了支持64位统计信息的多端口驱动程序如何响应此类 Oid 的查询。

### <a name="64-bit-query-of-a-64-bit-value"></a><a href="" id="-64-bit-query-of-a-64-bit-value"></a>64位值的64位查询

NDIS \_ OID \_ 请求 **InformationBufferLength** 大于或等于8。

微型端口驱动程序：

-   返回信息缓冲区中的64位值。

-   将 NDIS \_ OID \_ 请求 **BytesWritten** 设置为8。

-   \_ \_ 从[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)或[**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数返回 NDIS 状态 SUCCESS。

### <a name="32-bit-query-of-a-64-bit-value"></a><a href="" id="-32-bit-query-of-a-64-bit-value"></a>64位值的32位查询

NDIS \_ OID \_ 请求 **InformationBufferLength** 大于或等于4，小于8。

微型端口驱动程序：

-   返回在信息缓冲区中64位值的低32位。

-   将 NDIS \_ OID \_ 请求 **BytesWritten** 设置为4。

-   将 NDIS \_ OID \_ 请求 **BytesNeeded** 设置为8。

-   \_ \_ 从[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)或[**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数返回 NDIS 状态 SUCCESS。

### <a name="invalid-length-query-of-a-64-bit-value"></a>64位值的无效长度查询

NDIS \_ OID \_ 请求 **InformationBufferLength** 小于4。

微型端口驱动程序：

-   不返回信息缓冲区中的任何值。

-   将 NDIS \_ OID \_ 请求 **BytesWritten** 设置为0。

-   将 NDIS \_ OID \_ 请求 **BytesNeeded** 设置为8。

-   \_ \_ \_ 从[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)或[**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数返回 NDIS 状态无效长度。

 

