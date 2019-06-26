---
title: 从中间驱动程序发出设置和查询请求
description: 从中间驱动程序发出设置和查询请求
ms.assetid: bd049639-970c-43c8-8ef9-c5e75cc2d75f
keywords:
- 查询操作 WDK NDIS 中间
- 集运算 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f538bf67aa6865f269b5e3630d5c24ff40a1fc7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356248"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>从中间驱动程序发出设置和查询请求





中间的驱动程序的协议边缘可以颁发集和查询信息为基础的微型端口驱动程序的请求。 虚拟微型端口缘中间的驱动程序可以使用从基础驱动程序获取的信息来确定如何响应设置和查询请求。

若要取消的 OID 请求，请调用[ **NdisCancelOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest)函数。

有关详细信息响应来设置和查询请求，请参阅[中间驱动程序中的集和查询正在响应](responding-to-sets-and-queries-in-an-intermediate-driver.md)。 有关发出 OID 请求详细信息，请参阅[OID 协议驱动程序中的请求操作](oid-request-operations-in-a-protocol-driver.md)。

 

 





