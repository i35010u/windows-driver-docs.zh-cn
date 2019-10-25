---
title: 协议驱动程序同步 OID 请求
description: 本主题介绍微型端口适配器同步 OID 请求
ms.assetid: 34B88444-DDF1-4AEA-8277-3EA87CA7004A
keywords: 协议驱动程序同步 OID 请求接口，协议 driverSynchronous OID 调用，协议 driverWDK 同步 Oid，协议 driverSynchronous OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8dc84c841a9c5fed135ad43c34d7e54374a54a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844906"
---
# <a name="protocol-driver-synchronous-oid-requests"></a>协议驱动程序同步 OID 请求

为了支持同步 OID 请求路径，协议驱动程序调用[**NdisSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest)函数来发出同步 oid。

对于协议驱动程序，*同步 OID 请求接口*不同于规则和直接 OID 请求接口，该协议驱动程序不必实现异步*完成*回调函数。 这是因为路径的同步特性。 有关常规、直接和同步 Oid 之间的差异的详细信息，请参阅[NDIS 6.80 中的同步 Oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

> [!NOTE]
> NDIS 6.80 支持用于同步 OID 请求接口的特定 Oid。 不支持在 NDIS 6.80 和某些 NDIS 6.80 Oid 之前存在的 Oid。 若要确定是否可以在同步 OID 请求接口中使用 OID，请参见 "OID 引用" 页。

若要支持同步 OID 请求接口，请使用标准 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数与标准 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*NdisSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest) | [*NdisOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) |

