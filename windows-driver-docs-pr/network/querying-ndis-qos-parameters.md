---
title: 查询 NDIS QoS 参数
description: 查询 NDIS QoS 参数
ms.assetid: 875D39BA-D70D-4450-9F64-D08EAB54BDC2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cbf310d055dd8b48e91d7a204b98be4d472f02c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373127"
---
# <a name="querying-ndis-qos-parameters"></a>查询 NDIS QoS 参数


过量协议和筛选器驱动程序可通过以下方式在查询的网络适配器的 NDIS 服务质量 (QoS) 参数：

-   基础驱动程序可以查询通过对象标识符 (OID) 查询请求的操作的 NDIS QoS 参数[OID\_QOS\_OPERATIONAL\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451832)。

-   基础驱动程序可以查询通过 OID 查询请求的远程 NDIS QoS 参数[OID\_QOS\_远程\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451841)。

**请注意**  过量驱动程序无法查询本地的 NDIS QoS 参数。

 

有关本地、 远程和操作的 NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](overview-of-ndis-qos-parameters.md)。

NDIS 处理微型端口驱动程序这些 OID 请求，并返回请求中的 QoS 参数[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 NDIS 按以下方式处理这些 OID 请求：

-   NDIS 时处理的 OID 查询请求[OID\_QOS\_OPERATIONAL\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451832)，它将从上一个返回已缓存的操作的 NDIS QoS 参数[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示颁发的微型端口驱动程序。 其操作的 QoS 参数或者解决第一次或更高版本更改时，驱动程序将发出此状态指示。

    如果基础驱动程序将发出 OID 查询请求之前微型端口驱动程序问题[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示 NDIS 返回[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的所有成员 (除了**标头**成员) 将设置为零。

    **请注意**  NDIS 如果也会返回此结构微型端口驱动程序将发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)与状态指示[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的成员 （与异常**标头**成员) 设置为零。

     

-   NDIS 时处理的 OID 查询请求[OID\_QOS\_远程\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451841)，它将从上一个返回已缓存的远程 NDIS QoS 参数[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示颁发的微型端口驱动程序。 其远程 QoS 参数或者解决第一次或更高版本更改时，驱动程序将发出此状态指示。

    如果基础驱动程序将发出 OID 查询请求之前微型端口驱动程序问题[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示 NDIS 返回[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的所有成员 (除了**标头**成员) 将设置为零。

    **请注意**  NDIS 如果也会返回此结构微型端口驱动程序将发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)与状态指示[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的成员 （与异常**标头**成员) 设置为零。

     

 

 





