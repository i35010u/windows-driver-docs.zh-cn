---
title: 协议驱动程序同步 OID 请求
description: 本主题介绍微型端口适配器同步 OID 请求
ms.assetid: 34B88444-DDF1-4AEA-8277-3EA87CA7004A
keywords: 协议驱动程序同步 OID 请求接口，协议 driverSynchronous OID 调用时，协议 driverWDK 同步 Oid，协议 driverSynchronous OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 777d7a36cfb8366b9a08a2566302b512d4778d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385454"
---
# <a name="protocol-driver-synchronous-oid-requests"></a>协议驱动程序同步 OID 请求

若要支持同步 OID 请求路径，协议驱动程序调用[ **NdisSynchronousOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissynchronousoidrequest)函数发出同步 OID。

协议驱动程序，请*同步 OID 请求接口*不同于常规模式和直接 OID 请求接口，协议驱动程序不需要实现异步*完整*回调函数。 这是因为同步性质的路径。 有关常规中常规、 直接和同步 Oid 之间的差别的详细信息，请参阅[同步 OID 请求接口在 NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)。

> [!NOTE]
> NDIS 6.80 支持用于同步的 OID 请求接口的特定 Oid。 不支持 NDIS 6.80 和一些 NDIS 6.80 Oid 之前即已存在的 Oid。 若要确定是否可以在同步 OID 请求界面中使用 OID，请参阅 OID 引用页。

若要支持同步 OID 请求接口，使用标准的 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数和标准的 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*NdisSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissynchronousoidrequest) | [*NdisOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest) |

