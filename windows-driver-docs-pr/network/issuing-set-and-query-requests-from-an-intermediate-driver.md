---
title: 从中间驱动程序发出设置和查询请求
description: 从中间驱动程序发出设置和查询请求
keywords:
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53788cadc4d7eff440e393a8577e94f6c15de17b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789735"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>从中间驱动程序发出设置和查询请求





中间驱动程序的协议边缘可以发出对底层微型端口驱动程序的 set 和 query 信息请求。 中间驱动程序的虚拟微型端口边缘可以使用从基础驱动程序获取的信息来确定如何响应集和查询请求。

若要取消 OID 请求，请调用 [**NdisCancelOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest) 函数。

有关响应 set 和 query 请求的详细信息，请参阅 [响应中间驱动程序中的集和查询](responding-to-sets-and-queries-in-an-intermediate-driver.md)。 有关发出 OID 请求的详细信息，请参阅 [协议驱动程序中的 Oid 请求操作](oid-request-operations-in-a-protocol-driver.md)。

 

