---
title: 查询 64 位统计信息 OID
description: 查询 64 位统计信息 OID
ms.assetid: dc43c33d-12a7-4468-9980-a9015f43e068
keywords:
- 统计信息 Oid WDK 网络
- 64 位的统计信息 Oid WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d6277ef33c80f6c9fdbe2d249cd3df5af46aae8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577601"
---
# <a name="querying-64-bit-statistics-oids"></a>查询 64 位统计信息 OID


每秒 (Gbps) 为 1 千兆字节和更快地必须支持 64 位的所有微型端口驱动程序对于某些计数器 Oid 的统计信息。 所有 100 兆字节为单位每秒 (Mbps) 和更快的微型端口驱动程序应支持此类 Oid 的 64 位计数器。 无连接的微型端口驱动程序的统计信息 Oid 的详细信息，请参阅[General Statistics](https://msdn.microsoft.com/library/windows/hardware/ff552485)。 有关面向连接的微型端口驱动程序的此类 Oid 的详细信息，请参阅[Connection-Oriented 微型端口驱动程序的常规统计信息](https://msdn.microsoft.com/library/windows/hardware/ff552482)。

查询统计信息 OID 的请求者设置 NDIS\_OID\_请求**InformationBufferLength**到 4 （字节），指示 32 位统计信息请求或 8 （字节） 以指示 64 位统计信息请求。 微型端口驱动程序在其响应中设置 NDIS\_OID\_请求**BytesNeeded**微型端口驱动程序支持 (4 个 32 位) 或 8，64 位的统计信息值的大小。 微型端口驱动程序设置 NDIS\_OID\_请求**BytesWritten**到较小的**InformationBufferLength**值和大小的统计信息的微型端口驱动程序支持。

以下部分介绍支持 64 位的统计信息 Oid 的微型端口驱动程序如何响应查询的此类 Oid。

### <a href="" id="-64-bit-query-of-a-64-bit-value"></a>一个 64 位值的 64 位查询

NDIS\_OID\_请求**InformationBufferLength**大于或等于 8。

微型端口驱动程序：

-   返回信息缓冲区中的 64 位值。

-   设置 NDIS\_OID\_请求**BytesWritten**为 8。

-   返回 NDIS\_状态\_成功从其[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)或者[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数。

### <a href="" id="-32-bit-query-of-a-64-bit-value"></a>一个 64 位值的 32 位查询

NDIS\_OID\_请求**InformationBufferLength**到大于或等于 4 且小于 8。

微型端口驱动程序：

-   在信息缓冲区，较低的 64 位值的 32 位返回。

-   设置 NDIS\_OID\_请求**BytesWritten**为 4。

-   设置 NDIS\_OID\_请求**BytesNeeded**为 8。

-   返回 NDIS\_状态\_成功从其[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)或者[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数。

### <a name="invalid-length-query-of-a-64-bit-value"></a>一个 64 位值的长度无效的查询

NDIS\_OID\_请求**InformationBufferLength**小于 4。

微型端口驱动程序：

-   在信息缓冲区中不返回任何值。

-   设置 NDIS\_OID\_请求**BytesWritten**为 0。

-   设置 NDIS\_OID\_请求**BytesNeeded**为 8。

-   返回 NDIS\_状态\_无效\_长度从其[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)或[ **MiniportCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数。

 

 





