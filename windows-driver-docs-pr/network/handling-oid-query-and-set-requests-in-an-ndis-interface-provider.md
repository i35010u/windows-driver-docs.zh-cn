---
title: 在 NDIS 接口提供程序中处理 OID 查询和设置请求
description: 在 NDIS 接口提供程序中处理 OID 查询和设置请求
ms.assetid: 9ce51fc8-426f-4d36-8ee7-0a93b7b8439c
keywords:
- NDIS 网络接口 WDK，接口提供程序
- 网络接口 WDK，接口提供程序
- 接口提供程序 WDk 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73f68a9bd83ba7850c7147e0b15c0184db674b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379787"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>在 NDIS 接口提供程序中处理 OID 查询和设置请求





NDISIF 接口定义了多个接口参数 （包括统计计数器），可以查询或设置对应于 RFC 2863 中的信息。 NDIS 访问这些接口参数通过入口点的接口提供程序定义当调用[ **NdisIfRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)函数。 有关注册为接口提供程序的详细信息，请参阅[注册为接口提供程序](registering-as-an-interface-provider.md)。

接口参数由对象标识符 (Oid) 标识。 某些 Oid 是特定于接口提供程序。

以下主题介绍如何处理查询和设置接口参数的请求：

[处理一个接口对象查询请求](handling-an-interface-object-query-request.md)

[处理的接口对象会将请求设置](handling-an-interface-object-set-request.md)

 

 





