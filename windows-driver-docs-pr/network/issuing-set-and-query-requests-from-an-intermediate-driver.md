---
title: 发出从中间驱动程序集和查询请求
description: 发出从中间驱动程序集和查询请求
ms.assetid: bd049639-970c-43c8-8ef9-c5e75cc2d75f
keywords:
- 查询操作 WDK NDIS 中间
- 集运算 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54c843dae6ddbea99e3d7c128004b0f05aabe3a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546055"
---
# <a name="issuing-set-and-query-requests-from-an-intermediate-driver"></a>发出从中间驱动程序集和查询请求





中间的驱动程序的协议边缘可以颁发集和查询信息为基础的微型端口驱动程序的请求。 虚拟微型端口缘中间的驱动程序可以使用从基础驱动程序获取的信息来确定如何响应设置和查询请求。

若要取消的 OID 请求，请调用[ **NdisCancelOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561622)函数。

有关详细信息响应来设置和查询请求，请参阅[中间驱动程序中的集和查询正在响应](responding-to-sets-and-queries-in-an-intermediate-driver.md)。 有关发出 OID 请求详细信息，请参阅[OID 协议驱动程序中的请求操作](oid-request-operations-in-a-protocol-driver.md)。

 

 





