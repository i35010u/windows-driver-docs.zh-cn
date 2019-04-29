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
ms.openlocfilehash: 75832430bcdff619985f577b6e59fa5b632149e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379334"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>在 NDIS 接口提供程序中处理 OID 查询和设置请求





NDISIF 接口定义了多个接口参数 （包括统计计数器），可以查询或设置对应于 RFC 2863 中的信息。 NDIS 访问这些接口参数通过入口点的接口提供程序定义当调用[ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716)函数。 有关注册为接口提供程序的详细信息，请参阅[注册为接口提供程序](registering-as-an-interface-provider.md)。

接口参数由对象标识符 (Oid) 标识。 某些 Oid 是特定于接口提供程序。

以下主题介绍如何处理查询和设置接口参数的请求：

[处理一个接口对象查询请求](handling-an-interface-object-query-request.md)

[处理的接口对象会将请求设置](handling-an-interface-object-set-request.md)

 

 





